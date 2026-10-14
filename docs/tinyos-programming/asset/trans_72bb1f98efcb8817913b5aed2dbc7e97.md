

DetectorC 将预分频器设置为一个值（ATM128_ADC_PRESCALE_16），将 A/D 转换时间降低到 28 µs。这有可能将 SoundLocalizer 的精度提高 2.9 cm（85 µs · 340 m/s）。

由此产生的“响亮声音”检测代码很简单，但非常特定于 micaz 平台和 mts300 麦克风：

```
module DetectorC {
  uses interface Atm128AdcSingle;
  ...
}

implementation {
  // The threshold for a loud sound (determined experimentally)
  enum { THRESHOLD = 768 };

  void detect() {
    call Atm128AdcSingle.getData(... microphone A/D channel ...,
                          ATM128_ADC_VREF_OPF, FALSE,
                          ATM128_ADC_PRESCALE_16);
  }

  async event void Atm128AdcSingle.dataReady(uint16_t data, bool precise){
    /* If we’re the current ADC owner: check ADC completion events to
       see if the microphone is above the threshold */
    atomic
      if (granted)
        if (precise && data > THRESHOLD)
        {
          signal Detector.detected();
          ... post a task to release A/D converter, power off microphone
          and signal done ...
        }
        else
          detect();
      }
    ...
  }
```

dataReady 事件处理程序检查 DetectorC 当前是否拥有 A/D 转换器。如果是，则 A/D 结果高于阈值表示检测到响亮的声音。如果不是，则请求另一个 A/D 采样。

## 13.4 MicrophoneC

MicrophoneC 是控制传感器低级代码的相当典型的示例。mts300 麦克风硬件在图 13.4 中示意性地显示。麦克风通过来自微控制器的数字 I/O 引脚（MicPower）通电和断电。The

![](img/53ede4f4266a5731b93bff15d85fa06a_257_0.png)

### Figure 13.4 MTS300 microphone hardware.

原始麦克风输出经过一个放大器，其增益可通过 I²C 总线调节。最后，一个第二数字 I/O 引脚（MicMuxSel）选择原始麦克风输出和 4 kHz 音调检测器。²

因此，将麦克风通电用作“响亮声音”检测器需要物理上通电麦克风，选择原始麦克风输出并选择适当的放大器增益。最后，一旦这些步骤完成，麦克风应被留待预热 1.2 s（MICROPHONE_WARMUP）。这四个步骤由 MicrophoneC 的以下代码执行（省略了错误检查）：

```
module MicrophoneC {
  provides interface SplitControl;
  uses interface GeneralIO as MicPower;
  uses interface GeneralIO as MicMuxSel;
  uses interface I2CPacket<TI2CBasicAddr>;
  uses interface Resource as I2CResource;
}

implementation {
  enum {
    MIC_POT_ADDR = 0x5A, // Amplifier I2C address
    MIC_POT_SUBADDR = 0,
    MIC_GAIN = 64        // Desired gain
  };

  command error_t SplitControl.start() {
    // Power up the microphone
    call MicPower.makeOutput();
    call MicPower.set();
    // Select raw microphone output
    call MicMuxSel.makeOutput();
    call MicMuxSel.set();
    // Request the I2C bus to adjust gain
```

> ² The mts300 sensor board was originally designed in part for use in acoustic-based localization, and includes a 4 kHz tone generator.

```
call I2CResource.request();

return SUCCESS;
}

event void I2CResource.granted() {
    static uint8_t gainPacket[2] = { MIC_POT_SUBADDR, MIC_GAIN };

    // Send gain-control packet over I2C bus
    call I2CPacket.write(I2C_START | I2C_STOP, MIC_POT_ADDR,
                         sizeof gainPacket, gainPacket);
}

async event void I2CPacket.writeDone(error_t error, uint16_t addr,
                                     uint8_t length, uint8_t* data) {
    // Release I2C bus and wait for microphone to warm up (report failure
    // in case of error)
    call I2CResource.release();
    post gainOk(); // We're in async code, post a task for the warm up timer
}

task void gainOk() {
    call Timer.startOneShot(MICROPHONE_WARMUP);
}

event void Timer.fired() {
    // Microphone warmed up. Signal completion of startup.
    signal SplitControl.startDone(SUCCESS);
}
}
```

该麦克风通电代码当然特定于 mts300 传感器。然而，它实际上对使用相同传感器的其他平台来说相当可移植，因为它通过硬件无关的 GeneralIO 和 I2CPacket 接口访问所需的低级硬件功能（数字 I/O 引脚和 I²C 总线）。GeneralIO 接口提供配置、读取和写入典型微控制器数字 I/O 引脚的命令：

```
interface GeneralIO {
    async command void set();
    async command void clr();
    async command void toggle();
    async command bool get();
    async command void makeInput();
    async command bool isInput();
    async command void makeOutput();
    async command bool isOutput();
}
```

Listing 13.6  The GeneralIO digital I/O pin interface

