![](bbox=[0.15, 0.18, 0.9, 0.42])

# Figure 13.4 MTS300 microphone hardware.

raw microphone output goes through an amplifier, whose gain can be adjusted via an I²C bus. Finally, a second digital I/O pin (MicMuxSel) selects between raw microphone output and a 4 kHz tone detector.²

Powering on the microphone for use as a “loud sound” detector thus requires physically powering on the microphone, selecting raw microphone output and picking an appropriate amplifier gain. Finally, once these steps are complete, the microphone should be left to warm up for 1.2 s (MICROPHONE_WARMUP). These four steps are performed by the following code from MicrophoneC (error checking elided):

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