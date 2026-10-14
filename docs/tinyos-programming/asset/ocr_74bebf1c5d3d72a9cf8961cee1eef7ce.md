```
event void WarningTimer.fired() {
    if (call Leds.get() & LEDS_LED0)
    { // Red LED is on. Turn it off, will switch on again in 4096-64ms.
        call Leds.led0Off();
        call WarningTimer.startOneShot(WARN_INTERVAL - WARN_DURATION);
    }
    else
    { // Red LED is off. Turn it on for 64ms.
        call Leds.led0On();
        call WarningTimer.startOneShot(WARN_DURATION);
    }
}

event void Boot.booted() {
    // We just booted. Perform first LED transition.
    signal WarningTimer.fired();
}
```

# Listing 6.1 Anti-theft: simple flashing LED

Our application wants to show that it’s active and doing "something" using a red LED. However, an LED is relatively power hungry, so we don’t want to leave it on all the time. Instead, we will turn it on for 64 ms every four seconds. We accomplish this by using a single timer: if the LED is off, we switch it on and ask to be woken again in 64 ms; if the LED is on, we switch it off and ask to be woken in 3.936 s. This logic is implemented by the WarningTimer.fired event, based on the commands and events provided by the Timer and Leds interfaces:

```
interface Leds {
    async command void led0On();
    async command void led0Off();
    async command void led0Toggle();

    async command void led1On();
    async command void led1Off();
    async command void led1Toggle();

    async command void led2On();
    async command void led2Off();
    async command void led2Toggle();

    async command uint8_t get();
    async command void set(uint8_t val);
}
```

# Listing 6.2 The Leds interface