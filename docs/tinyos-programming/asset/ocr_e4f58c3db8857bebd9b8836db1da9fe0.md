However, dispatchers are often encapsulated in a generic configuration to simplify their use. Rather than have a component wire to a parameterized interface, it wires to a generic configuration that takes the parameter as an argument. For example, rather than wire directly to ActiveMessageC to receive packets, applications instantiates an AMReceiverC:

```
generic configuration AMReceiverC(am_id_t amid) {
  provides interface Receive;
  provides interface Packet;
  provides interface AMPacket;
}
implementation {
  components ActiveMessageImplP as Impl;

  Receive = Impl.Receive[amId];
  Packet = Impl;
  AMPacket = Impl;
}
```

Listing 10.1 AMReceiverC

Rewriting AppC using AMReceiverC gives:

```
configuration AppC ()
implementation {
  components AppP,
  new AMReceiverC(AM_CLEARIDMSG) as ClearId,
  new AMReceiverC(AM_SETIDMSG) as SetId;

  AppP.ClearIdMsg -> ClearId;
  AppP.SetIdMsg -> SetId;
}
```

# Known uses

The Active Messages networking layer (ActiveMessageC), and tree collection protocol (CollectionC) use a dispatcher for packet reception. They also provide a parameterized packet sending interface, so services can easily match packet sends to reception handlers.

The Atmel AT45DB family flash chip implementation uses a parameterized interface to map storage volume identifiers to storage volume characteristics (see the At45dbStorageManagerC component in Section 12.1.1).

The TinyOS 1.x Maté virtual machine uses a dispatcher to allow easy customization of instruction sets.

# Consequences

By leaving operation selection to nesC wirings, the dispatcher’s implementation remains independent of what an application supports. However, finding the full set of supported operations can require looking at many files. Sloppy operation identifier management