further illustrate the material, let's take a classic example that demonstrates the need for synchronization - the problem of producer-consumers or the problem of limited buffer ( bounded buffer ).

The formulation of the problem is simple. Suppose we have production threads and consumer threads. The manufacturer creates objects, the consumer receives them. The task is to synchronize their work so that the consumer cannot attempt to retrieve objects that have not yet been created, and the manufacturer cannot create more objects than the consumer can.

To synchronize flows, place a buffer of fixed length $n$ between the manufacturer and the consumer. The manufacturer can place objects on the buffer, the consumer - take them from there. If the consumer takes the object, it is removed from the buffer. There are several requirements to be met:

+   1. When the manufacturer or consumer is working with the buffer, the rest of the threads should wait for it to finish
+   2. When the manufacturer is trying to put an about object on the buffer and the buffer is full, it must wait until it appears in place
+   3. When a consumer tries to pick an about object of the buffer and the buffer is empty, it must wait until it is on ' ' appears about ' object

# Semaphores

Concept semaphore proposed in 1965 by E. Dijkstra - known Dutch specialist in Computer Books Science. Semaphores are the oldest synchronization primitives of those used in practice. Semaphore - a shared net ample integer counter asked for which initial value and determined following atomic operations: