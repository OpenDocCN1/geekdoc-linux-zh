
```c
event message_t *RDetection.receive(message_t *m, void* payload, uint8_t len){
  detection_msg_t *dmsg = payload;

  // Voting logic: if received message indicates global detection time
  // earlier than ours, switch off our LED and stop broadcasting
  if (dmsg->time < detectTime)
  {
    call Leds.led0Off();
    call VotingTimer.stop();
  }
  return m;
}
```

> ¹ `norace` 应谨慎使用，仅在你非常确定确实不存在任何可能竞争时才使用。

### 13.3 DetectorC

`DetectorC` 提供了一个 `Detector` 接口，用于检测大声响。其内部逻辑非常简单。首先，它打开麦克风电源。接下来，从 `Detector.start` 命令指定的时间开始，它反复采样麦克风的 A/D 通道，直到声音超过阈值。最后它关闭麦克风电源。麦克风的开关由下面描述的 `MicrophoneC` 组件提供的 `SplitControl` 接口控制。

如下面所述，`DetectorC` 使用 mica2 的 HAL 接口访问 A/D 转换器。A/D 转换器是一个共享驱动程序，其访问由 `Resource` 接口控制（第 11.2 节）。因此，当调用 `DetectorC` 的 `start (t0, dt)` 命令时，它必须打开麦克风电源，请求访问 A/D 转换器，并为本地时间 `t0+dt` 安排事件检测：

```c
module DetectorC {
  provides interface Detector;
  uses interface Alarm<TMicro, uint32_t>;
  uses interface Resource as AdcResource;
  uses interface SplitControl as Microphone;
  ...
}

implementation {
  bool granted, started; // Status of start request

  command void Detector.start(uint32_t t0, uint32_t dt) {
    atomic granted = started = FALSE;
    call Alarm.startAt(t0, dt);
    call Microphone.start();
    call AdcResource.request();
  }

  event void AdcResource.granted() {
    atomic granted = TRUE; // Note when ADC granted
  }

  event void Microphone.startDone(error_t error) {
    atomic started = error == SUCCESS; // Note if microphone started
  }

  async event void Alarm.fired() {
    // It’s time to detect a loud sound. If we didn’t get the ADC or
    // turn on the microphone in time, report a failed event detection.
    atomic
      if (granted && started)
      {
        call Leds.led1On();
        ... start detection ...
      }
      else
        post detectFailed();
  }
}
```

```c
task void detectFailed() {
  call Leds.led0Toggle();
  signal Detector.done(FAIL);
}
```

#### 清单 13.3 DetectorC：用于 SoundLocalizer 的响亮声音检测

`DetectorC` 使用 `Alarm<TMicro, uint32_t>` 接口以微秒精度调度事件检测。`Alarm` 接口是 `Timer` 的底层对应物：

```
interface Alarm<precision_tag, size_type> {
  // basic interface
  async command void start(size_type dt);
  async command void stop();
  async event void fired();

  // extended interface
  async command bool isRunning();
  async command void startAt(size_type t0, size_type dt);
  async command size_type getNow();
  async command size_type getAlarm();
}
```

#### 清单 13.4 Alarm 接口

与 `Counter` 一样，`Alarm` 接受类型参数，这些参数指明其时间单位的精度（毫秒（`TMilli`）、微秒（`TMicro`）等）和宽度（16 位（`uint16_t`）、32 位（`uint32_t`）等）。`Alarm` 与更高级的 `Timer` 接口（第 6.1.1 节）类似，不同之处在于它只提供单次定时器（`start`、`startAt`），它的命令都可以从中断处理程序中调用，并且它的 `fired` 事件在中断上下文中运行（所有接口函数都是 `async`）。

与 `Counter` 一样，TinyOS 没有提供 `Alarm<TMicro, uint32_t>` 接口的 HIL 组件，但 TEP102 [25] 也为提供 `Alarm` 接口的 HAL 组件的命名提供了指南。因此，以下针对 `DetectorC` 的接线应适用于所有具有 32 位微秒 `Alarm` 的平台：

```
components new AlarmMicro32C() as DAlarm;
DetectorC.Alarm -> DAlarm;
```

请注意，平台可能只提供有限数量的 `Alarm`。例如，`micaz` 只支持三个 32 位微秒 `Alarm`——每个 `micaz` `Alarm` 都需要自己的硬件定时器比较寄存器，而 `micaz` 的 `ATmega128` 微控制器每个硬件定时器只有三个比较寄存器。

通过同时调度 `Alarm`、麦克风上电和 A/D 转换器请求，`DetectorC.start` 允许这三个操作重叠执行（假设它们没有重叠的资源需求）。麦克风上电和 A/D 转换器请求的完成分别由 `started` 和 `granted` 布尔变量跟踪。`Alarm.fired` 在启动事件检测之前会检查这两个布尔值是否为真。如果不是，`DetectorC` 将检测失败报告回 `SynchronizerC`。`fired` 事件在中断上下文中运行，因此 `Alarm.fired`、`AdcResource.granted` 和 `Microphone.startDone` 中对 `started` 和 `granted` 变量的访问之间存在潜在的数据竞争。这种竞争风险是真实存在的（不同于 `SynchronizerC` 中的 `localDetectTime`），因此 `DetectorC` 使用 nesC 的原子语句来保护 `granted` 和 `started` 的读写。

为了精确检测响亮声音何时出现，`DetectorC` 应以尽可能高的速率对麦克风进行采样。此外，微控制器获取 A/D 样本与 `DetectorC` 检查该 A/D 值是否高于“响亮声音”阈值之间的抖动应尽可能小：例如，在样本获取与阈值测试之间增加 50–100 µs 的随机延迟，会给 `SoundLocalizer` 带来额外的 1.7cm（50 µs · 340 m/s）的不精确性。这两个因素都不支持使用面向传感器的高级 `Read` 接口（第 6.2.1 节）：`MicC`（mts300 传感器板上的麦克风组件）提供的 `Read` 开销相当高，并且在获取样本后会做相当多的处理。

使用 `MicStreamC` 组件提供的 `ReadStream` 接口（第 6.2.4 节）来实现 `DetectorC` 或许是可行的。该接口提供高频率、低抖动的采样，但使用起来相对复杂，并且不能直接指示每个样本获取的确切时间。相反，`DetectorC` 使用 `Atm128AdcC`，即 TinyOS 针对 `ATmega128` 的 HAL A/D 转换器组件。`Atm128AdcC` 是一个共享驱动（访问由 `Resource` 接口控制），并提供以下用于底层 A/D 访问的接口：
