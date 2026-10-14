```
command void led0Toggle();
...
```

# Listing 2.3 Simple nesC interfaces

The second part of Powerup, the PowerupAppC configuration, specifies how PowerupC is connected to TinyOS's services:

```
configuration PowerupAppC { 
implementation {
components MainC, LedsC, PowerupC;

MainC.Boot -> PowerupC.Boot;
PowerupC.Leds -> LedsC.Leds;
}
```

# Listing 2.4 PowerupAppC configuration in nesC

This says that the PowerupAppC application is built out of three components (modules or configurations), MainC (system boot), LedsC (LED control), and PowerupC (our powerup module). PowerupAppC explicitly specifies the connections (or wiring) between the interfaces provided and used by these components. When MainC has finished booting the system it signals the booted event of its Boot interface, which is connected by the wiring in PowerupAppC to the booted event in PowerupC. This event then calls the led0On command of its Leds interface, which is again connected (wired) by PowerupAppC to the Leds interface provided by LedsC. Thus the call turns on LED 0. The resulting component diagram is shown in Figure 2.1 – this diagram was generated automatically from PowerupAppC by nesdoc, nesC's documentation generation tool.

PowerupAppC illustrates the third major difference between C and nesC: wiring makes the connections expressed by linking the C version of Powerup with its "mote" library explicit. In the C version, Powerup calls a global function named led0_on which is connected to whatever library provides a function with the same name; if two libraries

![](bbox=[0.25, 0.82, 0.65, 0.95])

# Figure 2.1 Wiring Diagram for Powerup application