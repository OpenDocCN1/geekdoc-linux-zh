# Components and interfaces

![](bbox=[0.183, 0.122, 0.617, 0.287])

**Figure 3.3** The Init and Boot interfaces.

and PowerupC, PowerupC is a user of Boot, while MainC is a provider of Boot:

```
configuration MainC {
  provides interface Boot;
  uses interface Init as SoftwareInit;
}

module PowerupC {
  uses interface Boot;
  uses interface Leds;
}
```

Listing 3.8 Signatures of MainC and PowerupC

Boot has a single event, Boot.booted. MainC provides Boot, so it signals the event when a node has booted successfully. This signaling is a function call: the boot sequence calls Boot.booted on all of the components that want to know when the system has come up. If a component -- such as PowerupC -- wants to know when the node has booted, it uses the Boot interface.

Commands have the opposite implementation direction as events. Users call commands and providers implement them. MainC uses Init so it can initialize software components before booting: it calls SoftwareInit.init on the components that need initialization. Similarly, as PowerupC uses Leds, it can call commands such as Leds.led0On. Conversely, a provider of Leds, such as LedsP, must implement the Leds commands.

Figure 3.3 shows the Boot and Init interfaces graphically. Init has a single command, init. A user of the Init interface can call Init.init, while a provider of the Init interface must implement Init.init. Conversely, a user of the Boot interface must implement the booted event, while a provider of the interface can signal Boot.booted.

At this point, the distinction between commands and events might seem pointless. After all, providing an interface with a command is the same as using an interface with an event. In the case of interfaces which only have commands or events but not both, this is true, and distinction is more for presentation and legibility. Providing an interface means providing a service, whether that be controlling the LEDs on a node or notifying components when the system has booted. Using an interface means using that service. However, as we'll soon see, many interesting interfaces have both commands and events, representing a relationship between two components where both can call the other.