
The precision, sampling rate, and jitter requirements vary greatly from application to application: a simple environmental monitoring application might sample a few sensors every 5 minutes, while a seismic monitoring system might sample acceleration at a few kHz for several seconds, but only once per day.

As a result, TinyOS does not offer a single unified way of accessing all sensors. Instead, it defines a set of common interfaces for sampling sensors, and a set of guidelines for building components that give access to particular sensors.

### 6.2.1  Simple sampling

The two main sampling interfaces are Read (which we saw in Section 3.4) and ReadStream, covering respectively the case of acquiring single samples and sampling at a fixed rate (with low jitter). As a reminder, Read provides a split-phase read command, that initiates sampling, and a readDone event that reports the sample value and any error that occurred, for an arbitrary type val_t.

```
interface Read<val_t> {
  command error_t read();
  event void readDone(error_t result, val_t val);
}
```

Listing 6.7  The Read interface

In common with most TinyOS split-phase interfaces, you can only start a single sample operation at a time, i.e. calling read again before readDone is signaled will fail (read will not return SUCCESS). However (again in common with other split-phase interfaces), it is legal to call read from the readDone event handler, making it easy to perform back-to-back reads.

We can make our anti-theft application more realistic by detecting theft attempts. A first simplistic attempt is based on the observation that stolen items are often placed in bags and pockets, i.e. dark locations. The DarkC module detects dark locations by periodically (every DARK_INTERVAL) sampling a light sensor (using the Read interface) and checking whether the light value is below some threshold (DARK_THRESHOLD). It then reports theft by turning the yellow LED (LED 2 on the micaZ) on:

```
module DarkC {
  uses {
    interface Boot;
    interface Leds;
    interface Timer<TMilli> as TheftTimer;
    interface Read<uint16_t> as Light;
  }
}
implementation {
enum { DARK_INTERVAL = 256, DARK_THRESHOLD = 200 };

event void Boot.booted() {
  call TheftTimer.startPeriodic(DARK_INTERVAL);
}

event void TheftTimer.fired() {
  call Light.read(); // Initiate split-phase light sampling
}

/* Light sample completed. Check if it indicates theft */
event void Light.readDone(error_t ok, uint16_t val) {
  if (ok == SUCCESS && val < DARK_THRESHOLD)
    call Leds.led2On(); /* ALERT! ALERT! */
  else
    call Leds.led2Off(); /* Don't leave LED permanently on */
}
}
```

Listing 6.8 Anti-theft: detecting dark conditions

We could have implemented dark-detection within the existing AntiTheftC module, and reused the existing WarningTimer. While this would slightly reduce CPU and storage requirements in the timer subsystem, it would increase code complexity in AntiTheftC by mixing code for two essentially unrelated activities. It is generally better to have a single module do one task (blinking an LED, detecting dark conditions) well rather than build a complex module which tries to handle many tasks, paying a significant price in increased complexity.

As is, DarkC is very simple: it initiates periodic sampling in its booted event. Four times a second, TheftTimer.fired requests a new light sample using the split-phase Read interface representing the light sensor (Light). If the sampling succeeds (ok == SUCCESS), then the light is compared to the threshold indicating dark conditions and hence theft. DarkC does not check the error return from Light.read, as there is no useful recovery action when light sampling cannot be initiated – it will retry the detection in 1/4s anyway.

### 6.2.2 Sensor components

Sensors are represented in TinyOS by generic components offering the Read and/or ReadStream interfaces, and possibly other sensor-specific interfaces (e.g. for calibration). A single component normally represents a single sensor, e.g. PhotoC for the light sensor on the mts310 sensor board:

```
generic configuration PhotoC() {
  provides interface Read<uint16_t>;
}
```

If two sensors are closely related (e.g. the X and Y axis of an accelerometer) they may be offered by a single component. Similarly, if a sensor supports both single (Read)
