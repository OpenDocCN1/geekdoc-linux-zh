```
Packet = AM;
AMPacket = AM;
PacketAcknowledgements = AM;
}
```

# Listing 10.3 Telos ActiveMessageC

The Ctp and Lqi tree-routing protocols provide CtpCollectionC and LqiCollectionC components in separate directories. They also provide a placeholder CollectionC component that wires to CtpCollectionC or LqiCollectionC. Components that wish to use the default tree-collection wire to CollectionC, leaving the choice of tree-routing protocol to the application. Components that wish to use a specific tree-collection algorithm wire, e.g. to CtpCollectionC.

# Known uses

Hardware-independent abstractions which have multiple implementations are often placeholders. For instance, each platform must map the ActiveMessageC and HiiTimerMilliC components to a platform-specific implementation. In many cases, like CC2420ActiveMessageC, this implementation is specific to a particular radio chip but portable across mote platforms. Leaving the mapping of ActiveMessageC to the platform can be important if a mote has two radios and one should be used as the default.

CollectionC is the placeholder for tree-collection routing protocols, DisseminatorC is the placeholder for key-value dissemination protocols, and RandomC is the placeholder for random-number generation.

# Consequences

The key aspects of the Placeholder pattern are:

+   - Establishes a global name that users of a common service can wire to.
+   - Allows you to specify the implementation of the service on an application-wide basis.
+   - Does not require every component to use the Placeholder’s implementation.

By adding a level of naming indirection, a Placeholder provides a single point at which you can choose an implementation. Placeholders create a global namespace for implementation-independent users of common system services. As using the Placeholder pattern generally requires every component to wire to the Placeholder instead of a concrete instance, incorporating a Placeholder into an existing application can require modifying many components. However, the nesC compiler optimises away the added level of wiring indirection, so a Placeholder imposes no run-time overhead. The Placeholder supports flexible composition and simplifies use of alternative service implementations.

# Related patterns

+   - Dispatcher: a placeholder allows an application to select an implementation at compile-time, while a dispatcher allows it to select an implementation at run-time.