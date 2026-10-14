```
FileDir = Dir.FileDir;
FileRename = Rename.FileRename;
FileDelete = Delete.FileDelete;
// Wiring of operations to sub-services omitted
}
```

# Listing 10.4 The Matchbox facade

# Sample 2.x code

The CC2420 radio stack is broken up into three call paths: control, transmission, and reception. The top-level CC2420CsmaC component presents these three paths together as a single abstraction using a Facade:

```
configuration CC2420CsmaC {
  provides interface Init;
  provides interface SplitControl;

  provides interface Send;
  provides interface Receive;
  provides interface PacketAcknowledgements as Acks;

  uses interface AMPacket;
}
implementation {
  components CC2420CsmaP as CsmaP;
  Init = CsmaP;
  SplitControl = CsmaP;
  Send = CsmaP;
  Acks = CsmaP;
  AMPacket = CsmaP;

  components CC2420ControlC;
  Init = CC2420ControlC;
  AMPacket = CC2420ControlC;
  CsmaP.Resource -> CC2420ControlC;
  CsmaP.CC2420Config -> CC2420ControlC;

  components CC2420TransmitC;
  Init = CC2420TransmitC;
  CsmaP.SubControl -> CC2420TransmitC;
  CsmaP.CC2420Transmit -> CC2420TransmitC;
  CsmaP.CsmaBackoff -> CC2420TransmitC;

  components CC2420ReceiveC;
  Init = CC2420ReceiveC;
  Receive = CC2420ReceiveC;
  CsmaP.SubControl -> CC2420ReceiveC;

  components RandomC;
  CsmaP.Random -> RandomC;
```