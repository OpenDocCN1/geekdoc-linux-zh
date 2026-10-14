Unlike standard components, generics can only be named by the configuration that instantiates them. For example, in the case of MyAppC, no other component can wire to the BitVectorC that it instantiates. The generic is private to MyAppC. The only way it can be made accessible is to wire its interfaces – in the case of MyAppC, the bit vector is made accessible to MyAppP only. One way to make an instance generally available is to create a singleton configuration and exporting the necessary interfaces. For example, let’s say you needed a bit vector to keep track of which of 37 system services are running or not. You want many components to be able to access this vector, but BitVectorC is a generic. So you write a component like this:

```
configuration SystemServiceVectorC {
  provides interface BitVector;
}
implementation {
  components MainC, new BitVectorC(37);
  MainC.SoftwareInit -> BitVectorC;
  BitVector = BitVectorC;
}
```

Listing 8.2 The fictional component SystemServiceVectorC

Now many components can refer to this particular bit vector. SystemServiceVectorC could have exported BitVectorC.Init rather than wiring it to MainC, but that would have just required this wiring to be performed elsewhere. While you can make a singleton out of a generic by instantiating it within one, the opposite is not true: a component is either instantiable or not.

# 8.2 Writing generic modules

As the examples above showed, the body of a generic module (configuration) is simply a module (configuration) which can use the generic’s arguments as types, constants, etc. Another example is the queue implementation, QueueC:

```
generic module QueueC(typedef queue_t, uint8_t queueSize) {
  provides interface Queue<queue_t>;
}
implementation {
  queue_t queue[queueSize];
  uint8_t head = 0, tail = 0, size = 0;

  command queue_t Queue.head() {
    return queue[head];
  }
  ...
```

Listing 8.3 QueueC excerpt