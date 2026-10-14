Adding a buffer to the LogStorageC component forces all logging applications to allocate the buffer. As some applications may not able to spare the RAM, this is undesirable. Providing two versions, buffered and unbuffered, replicates code, reducing reuse, and increasing the possibility of incomplete bug fixes. It is possible that several implementers of the interface – any component that provides LogWrite – may benefit from the added functionality. Having multiple copies of the buffering version, spread across several services, further replicates code.

There are two traditional object-oriented approaches to this problem: inheritance, which defines the relationship at compile-time through a class hierarchy, and decorators, which define the relationship at run-time through encapsulation. As nesC is not an object-oriented language, and has no notion of inheritance, the former option is not possible. Similarly, run-time encapsulation is not readily supported by nesC’s static component composition model and imposes overhead in terms of pointers and call forwarding. However, we can use nesC’s component composition and wiring to provide a compile-time version of the Decorator.

A Decorator component is typically a generic module that provides and uses the same interface type, such as LogWrite. The provided interface adds functionality on top of the used interface. For example, we show a BufferedLogC component that sits on top of a LogWrite provider. It implements its additional functionality by aggregating several writes to BufferedLogC writes into a single write to the underlying LogWrite interface.

Using a Decorator can have further benefits. In addition to augmenting existing interfaces, they can introduce new ones that provide alternative abstractions. For example, BufferedLogC provides a synchronous (not split phase) FastLog interface; a call to FastLog writes directly into the buffer.

Finally, separating added functionality into a Decorator allows it to apply to any implementation. For example, a packet send queue Decorator can be interposed on top of any networking abstraction that provides the Send interface; this allows flexible interpositioning of queues and queueing policies in a networking system.

# Applicable when

+   - You wish to extend the functionality of an existing component without changing its implementation, or
+   - You wish to provide several variants of a component without having to implement each possible combination separately.

# Structure

![](bbox=[0.25, 0.0011200000000000001, 0.85, 0.00198])