
shows the resulting components: AMQueueEntryP implements the per-client logic needed to queue packets for a particular AM identifier, AMQueueImplP implements the queue, and AMQueueP wires the queue to ActiveMessageC. At run-time, a typical execution is:

- 1. Client calls AMSenderC's AMSend.send.
- 2. This calls end in module AMQueueEntryP, which stores the length, AM identifier, and destination in the packet.
- 3. AMQueueEntryP is a client of AMQueueImplP and calls Send.send with its client identifier.
- 4. AMQueueImplP checks that the client's queue entry is free and puts the packet into it.
- 5. Some time later, AMQueueImplP pulls the packet off the queue and calls AMSend.send on ActiveMessageC with the parameters that AMQueueEntryP stored.
- 6. When ActiveMessageC signals AMSend.sendDone, AMQueueImplP signals Send.sendDone to AMQueueEntryP, which signals AMSend.sendDone to the original calling component.

This is the code for AMSenderC:

```
generic configuration AMSenderC(am_id_t AMId) {
  provides {
    interface AMSend;
    interface Packet;
    interface AMPacket;
    interface PacketAcknowledgements as Acks;
  }
}

implementation {
  components new AMQueueEntryP(AMId) as AMQueueEntryP;
  components AMQueueP, ActiveMessageC;

  AMQueueEntryP.Send -> AMQueueP.Send[unique(UQ_AMQUEUE_SEND)];
  AMQueueEntryP.AMPacket -> ActiveMessageC;

  AMSend = AMQueueEntryP;
  Packet = ActiveMessageC;
  AMPacket = ActiveMessageC;
  Acks = ActiveMessageC;
}
```

A send queue entry is responsible for storing send information in a packet:

```
generic module AMQueueEntryP(am_id_t amId) {
  provides interface AMSend;
  uses{
    interface Send;
    interface AMPacket;
  }
}

implementation {

  command error_t AMSend.send(am_addr_t dest,
                          message_t* msg,
                          uint8_t len) {
    call AMPacket.setDestination(msg, dest);
    call AMPacket.setType(msg, amId);
    return call Send.send(msg, len);
  }

  command error_t AMSend.cancel(message_t* msg) {
    return call Send.cancel(msg);
  }

  event void Send.sendDone(message_t* m, error_t err) {
    signal AMSend.sendDone(m, err);
  }

  command uint8_t AMSend.maxPayloadLength() {
    return call Send.maxPayloadLength();
  }

  command void* AMSend.getPayload(message_t* m) {
    return call Send.getPayload(m);
  }
}
```

Listing 9.14 AMSendQueueEntryP

The queue itself sits on top of ActiveMessageC:

```
configuration AMQueueP {
  provides interface Send[uint8_t client];
}

implementation {
  components AMQueueImplP, ActiveMessageC;

  Send = AMQueueImplP;
```

```
AMQueueImplP.AMSend -> ActiveMessageC;
AMQueueImplP.AMPacket -> ActiveMessageC;
AMQueueImplP.Packet -> ActiveMessageC;

}
```

Listing 9.15 AMQueueP

Finally, within AMSendQueueImplP, the logic to send a packet looks like this:

```
nextPacket();
if (current == QUEUE_EMPTY) {
    return;
}
else {
    message_t * msg;
    am_id_t id;
    am_addr_t addr;
    uint8_t len;
    msg = queue[current];
    id = call AMPacket.getType(msg);
    addr = call AMPacket.getDestination(msg);
    len = call Packet.getLength(msg);
    if (call AMSend.send(id, addr, msg, len) == SUCCESS) {
        ...
    }
    ...
}
```

Listing 9.16 AMSendQueueImplP pseudocode

## 9.2.4 BlockStorageC

One of the most difficult parts of nesC programming is using parameterized interfaces and managing their keyspaces. As we saw in Section 6.5, BlockStorageC is one of TinyOS’s three storage abstractions, and provides random read/write access to a storage volume (a contiguous area on a flash chip). BlockStorageC is a good example of using generics, because it is non-trivial use of wiring to build an abstraction from underlying components. BlockStorageC deals with four different sets of parameterized interfaces.

Every volume has a unique identifier, and every BlockStorageC is associated with a single volume. However, there can be multiple BlockStorageC components accessing multiple volumes, and not all volumes may have BlockStorageC components (they may be unused or accessed by a different abstraction). A client has to be associated with a volume so that the underlying code can generate an absolute offset into the chip from a relative offset within a volume. For example, if a 1 MB flash chip is divided into two 512 KB volumes, then address 16k on volume 1 is address 528k on the chip. This means that there are at least two keyspaces. The first keyspace is the volume ID keyspace, and the second is the client ID keyspace.
