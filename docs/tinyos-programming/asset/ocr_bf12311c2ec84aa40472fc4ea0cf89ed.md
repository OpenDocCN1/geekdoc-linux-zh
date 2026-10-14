since the parameter is a value, unlike a name it can be configured and set. For example, a component can do something like this:

```
```nesC
#ifdef ROUTING_TYPE
#define ROUTING_TYPE 201
#endif

RouterP.AMSend -> PacketSenderC.AMSend[ROUTING_TYPE];
```
```

Listing 8.18  Defining a parameter

Pushing constants into wiring avoids the pitfalls of using run-time parameters. Because the constant is set at compile-time, nesC can automatically fill it in and dispatch based on it simplifying the code and improving the efficiency of outgoing function invocations. Note that you can also wire entire parameterized interfaces:

```
```nesC
configuration CC2420ActiveMessageC {
  provides interface AMSend[am_id_t id];
}
{ ... }
configuration ActiveMessageC {
  provides interface AMSend[am_id_t id];
}
implementation {
  components CC2420ActiveMessageC;
  AMSend = CC2420ActiveMessageC;
}
```
```

Listing 8.19  Wiring full parameterized interface sets

**Programming Hint 18**  USE A PARAMETERIZED INTERFACE WHEN YOU NEED TO DISTINGUISH CALLERS OR WHEN YOU HAVE A COMPILE-TIME CONSTANT PARAMETER.

# 8.3.3  Defaults

Because a module’s call points are resolved in configurations, a common compile error in nesC is to forget to wire something. The equivalent in C is to forget to include a library in the link path, and in Java it’s to include a jar. Usually, a dangling wire represents a bug in the program. With parameterized interfaces, however, often they don’t.

Take, for example, the Receive interface of ActiveMessageC. Most applications receive a few AM types, maybe 15 at most: they don’t respond to or use every protocol ever developed. However, there’s this call in CC2420ActiveMessageP:

```
```nesC
return signal Receive.receive[call AMPacket.type(msg)]
(msg, payload, len - CC2420_SIZE);
```
```