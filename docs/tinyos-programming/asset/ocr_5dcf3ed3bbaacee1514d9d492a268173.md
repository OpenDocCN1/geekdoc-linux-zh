```
```text
        call Leds.led2On(); /* ALERT! ALERT! */
        reportTheft()
    }
}
```
```

Listing 6.16 Anti-Theft: changing settings

# 6.3.3  Selecting a communication stack

Nothing in the code seen so far specifies which communication stack is used for theft reports, or which AM types distinguish theft reports from settings updates. This information is specified in configurations, by wiring to the components representing the desired communication stack: these components have compatible signatures, making it easy to switch between stacks:

```
```text
configuration ActiveMessageC {
  provides interface SplitControl;
  ...
}
generic configuration AMSenderC(am_id_t id) {
  provides interface AMSend;
  ...
}
generic configuration AMReceiverC(am_id_t id) {
  provides interface Receive;
  ...
}

configuration SerialActiveMessageC{
  provides interface SplitControl;
  ...
}
generic configuration SerialAMSenderC(...){
  provides interface AMSend;
  ...
}
generic configuration SerialAMReceiverC(...){
  provides interface Receive;
  ...
}
```
```

Listing 6.17 Serial vs Radio-based AM components

ActiveMessageC contains the SplitControl interface to start and stop the communication stack. Instantiating AMSenderC with a particular AM type creates a component that provides an AMSend interface that will queue a single packet for transmission, independently of all other AMSenderC instances. This makes life simpler for modules using AMSend: as long as they only send one packet at a time, they can be assured that they can always enqueue their packet. Finally, instantiating AMReceiverC with AM type k and wiring the Receive interface to your code automatically dispatches received packets of type k to your Receive.receive event handler.

The anti-theft application uses radio-based communication (the mts300 sensor board physically interfaces with a serial connection):

```
```text
enum { AM_THEFT = 42, AM_SETTINGS = 43 };
...
components ActiveMessageC;
components new AMSenderC(AM_THEFT) as SendTheft;
components new AMReceiverC(AM_SETTINGS) as ReceiveSettings;
MovingC.CommControl -> ActiveMessageC;
```
```