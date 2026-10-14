# 3.3.1 Modules

Module implementations are written in nesC’s dialect of the C language. At the level of single statements, nesC is almost identical to C. It differs mainly in how code calls functions and variable scoping. As a component must implement commands for interfaces it provides and events for interfaces it uses, a module’s code must define these functions. For example, this is the module code for the PowerupC module:

```
module PowerupC {
  uses interface Boot;
  uses interface Leds;
}
implementation {
  event void Boot.booted() {
    call Leds.led0On();
  }
}
```

Listing 3.15 PowerupC module code

As PowerupC uses the Boot interface, and Boot has a single event, booted, PowerupC must provide an implementation: event void Boot.booted() { ... }. When the provider of Boot signals this event, PowerupC turns on LED 0 of the Leds interface. Modules invoke commands with the call keyword and invoke events with the signal keyword. For this reason, you’ll often see the terms “call commands” and “signal events.” The Leds interface has three LEDs, mostly for historical reasons. They are named led0, led1, and led2. In addition to turning LEDs on (e.g., led0On), the Leds interface allows you to turn them off (e.g., led0Off) and toggle them (e.g., led0Toggle). For example, this component will cause system boot to enter an infinite loop that toggles all three LEDs:

```
module PowerupToggleC {
  uses interface Boot;
  uses interface Leds;
}
implementation {
  event void Boot.booted() {
    while (1) {
      call Leds.led0Toggle();
      call Leds.led1Toggle();
      call Leds.led2Toggle();
    }
  }
}
```

Listing 3.16 The module PowerupToggleC

For PowerupToggleC to do anything, we must specify which components providing Boot and Leds we want to connect PowerupToggleC to. This is the role of the PowerupToggleAppC configuration which we will write next.