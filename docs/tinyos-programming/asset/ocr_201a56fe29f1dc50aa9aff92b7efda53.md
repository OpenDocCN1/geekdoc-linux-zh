```
generic configuration ConfigStorageC( volume_id_t volume_id ) {
    provides interface Mount;
    provides interface ConfigStorage;
}
```

Because flash storage implementations are chip-specific, you usually find them in a tos/chips directory. For example, the mica family of nodes has an AT45DB-family flash chip: when you use one of the above abstractions on a mica, you use the components in tos/chips/at45db.

# A.6 Data structures

TinyOS has component implementations of a few commonly used data structures. All of these can be found in tos/system.

# A.6.1 BitVectorC

BitVectorC provides the abstraction of a bit vector. It takes a single parameter, the width of the vector. The BitVector interface has commands for getting, setting, clearing, and toggling individual bits or all of the bits at once. Because of nesC’s heavy inlining, using BitVectorC is preferable to writing your own bit vector macros within a component. BitVectorC allocates ⌈N/8⌉ bytes for an N-bit wide vector.

```
generic module BitVectorC(uint16_t max_bits) {
    provides interface BitVector;
}
```

# A.6.2 QueueC

QueueC provides the abstraction of a queue of items with a fixed maximum size. It takes two parameters: the type of the items it stores and the maximum size of the queue. The Queue interface has commands for enqueuing items on the end of the queue, dequeuing the head of the queue, and commands for checking the queue size. It also allows random-access lookup: you can scan the queue.

```
generic module QueueC(typedef queue_t, uint8_t QUEUE_SIZE) {
    provides interface Queue<queue_t>;
}
```