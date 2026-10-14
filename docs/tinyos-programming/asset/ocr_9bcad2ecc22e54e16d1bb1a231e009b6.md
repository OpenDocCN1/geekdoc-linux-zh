accessed by the GeneralIO interface. PlatformLedsC provides three such IO lines, and uses an Init interface which is wired to LedsP.Init to initialize LedsP at system boot time.

From a programming standpoint, the configuration operators have two very different purposes. The -> and <- operators combine existing components, completing existing signatures. The = operator defines how a configuration’s interfaces are implemented. Like a module, a configuration is an abstraction defined by a signature. Modules directly implement their functions (events from used interfaces, commands from provided interfaces). Configurations delegate implementations to other components using the = operator. For example, LedsC delegates the implementation of the Leds interface to LedsP.

# 4.1.3 Namespace management

We saw in Section 3.1.2 the use of as to manage the names in a component signature, e.g., MainC has

```
uses interface Init as SoftwareInit;
```

The as keyword can also be used within configurations. Because nesC components are in a global namespace, sometimes they have very long and descriptive names. For example, the lowest level (byte) SPI bus abstraction on the ATmega128 is HplAtm128SpiC, which means, “This is the hardware presentation layer component of the ATmega128 SPI bus.” Typing that in a configuration is painful and not very easy to read. So, the slightly higher level abstraction, the configuration Atm128SpiC, names it like this:

```
component HplAtm128SpiC as HplSpi;
```

which makes the wiring significantly clearer. As was the case with interfaces, all components statements have an implicit use of as:

```
components MainC;
```

is just shorthand for

```
components MainC as MainC;
```

Another example of using as to clarify a configuration is found in CC2420ReceiveC, the receive path of the CC2420 radio. This configuration wires packet logic to things like interrupts and status pins:

```
configuration CC2420ReceiveC (...) 
implementation { 
  components CC2420ReceiveP; 
  components new CC2420SpiC() as Spi;
```