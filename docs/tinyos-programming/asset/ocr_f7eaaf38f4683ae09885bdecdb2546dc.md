the precision, sampling rate, and jitter requirements vary greatly from application to application: a simple environmental monitoring application might sample a few sensors every 5 minutes, while a seismic monitoring system might sample acceleration at a few kHz for several seconds, but only once per day.

As a result, TinyOS does not offer a single unified way of accessing all sensors. Instead, it defines a set of common interfaces for sampling sensors, and a set of guidelines for building components that give access to particular sensors.

# 6.2.1  Simple sampling

The two main sampling interfaces are Read (which we saw in Section 3.4) and ReadStream, covering respectively the case of acquiring single samples and sampling at a fixed rate (with low jitter). As a reminder, Read provides a split-phase read command, that initiates sampling, and a readDone event that reports the sample value and any error that occurred, for an arbitrary type val_t.

```
interface Read<val_t> {
  command error_t read();
  event void readDone(error_t result, val_t val);
}
```

*Listing 6.7  The Read interface*

In common with most TinyOS split-phase interfaces, you can only start a single sample operation at a time, i.e. calling read again before readDone is signaled will fail (read will not return SUCCESS). However (again in common with other split-phase interfaces), it is legal to call read from the readDone event handler, making it easy to perform back-to-back reads.

We can make our anti-theft application more realistic by detecting theft attempts. A first simplistic attempt is based on the observation that stolen items are often placed in bags and pockets, i.e. dark locations. The DarkC module detects dark locations by periodically (every DARK_INTERVAL) sampling a light sensor (using the Read interface) and checking whether the light value is below some threshold (DARK_THRESHOLD). It then reports theft by turning the yellow LED (LED 2 on the micaz) on:

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
```