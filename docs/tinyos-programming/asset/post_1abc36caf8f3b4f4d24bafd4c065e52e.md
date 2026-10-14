
Thinking through this problem from a programming standpoint, the receiver part of the radio stack needs to go through these steps:

- Read the packet out of the radio
- Inspect the packet to see if it should send an acknowledgement
- Switch the radio to transmit mode
- Send the acknowledgement
- Return the radio to receive mode

Each of these steps is typically a separate split-phase operation. On the CC2420 radio, for example, each operation requires sending a command that reads or writes data over an SPI bus. This SPI bus, however, is shared across many chips and subsystems: a flash storage driver might want to use the SPI bus to read data at the same time a node is receiving a packet. We can’t rely on the SPI bus component to schedule multiple outstanding requests, as it might try interleaving a large flash write operation between two of the radio stack’s. We need a way for the radio stack to request exclusive access to the bus so it can quickly perform its five operations, then release the bus for others to use.

There are numerous other cases where low-level systems need exclusive access to a hardware or software resource, either for correctness or latency; we’ll cover a few examples later.

## 11.2.2 Split-phase locks

TinyOS supports exclusive access to resources through split-phase locks. Traditionally, locks such as mutexes and semaphores are blocking constructs that protect critical sections or shared data structures. However, as TinyOS does not have blocking calls, its locks must be split-phase. A component calls a command to request a power lock and receives an event when it acquires the lock. For historical reasons, the lock interface is named Resource:

```
interface Resource {
  async command error_t request();
  async command error_t immediateRequest();
  event void granted();
  async command void release();
  async command uint8_t getId();
}
```

Listing 11.13 The Resource interface

To acquire a lock, a component typically calls request. At some point later, it receives a granted event, signaling that it can use whatever the lock protects. The command immediateRequest is an optimization: it allows a component to acquire an idle lock in a single-phase operation. If immediateRequest returns FAIL then the lock is already held and the component must call request. Components release a lock with the release command.

Abstractions that require locking typically provide the Resource interface. Calling functional interfaces without holding the lock is typically forbidden, and may cause bugs or undesirable system behavior. For example, this is the abstraction nodes with an MSP430 microcontroller provide for an SPI bus:

```
generic configuration Msp430Spi0C() {
  provides interface Resource;
  provides interface SpiByte;
  provides interface SpiPacket;
  uses interface Msp430Spi0CConfiguration;
}
```

Listing 11.14 Msp430Spi0C signature

Similarly, this is the abstraction for the ADC:

```
generic configuration Msp430Adc12ClientC() {
  provides {
    interface Resource;
    interface Msp430Adc12SingleChannel;
    interface Msp430Adc12MultiChannel;
    interface Msp430Adc12Overflow;
  }
}
```

Listing 11.15 Msp320Adc12ClientC signature

## 11.2.3 Lock internals

TinyOS power locks manage concurrency, energy, and configuration of shared hardware resources. Power locks have three sub-components:

- an *arbiter*, which controls the locking policy;
- a *power manager*, which controls the energy policy;
- and one or more *configurators*, which configure hardware for a client.

Figure 11.1 shows how these three parts fit together. The arbiter is the central point of control. An arbiter receives lock requests from clients, and calls the power manager and configurators based on those requests. Locks use parameterized interfaces and unique() to maintain a queue of pending lock requests. Each lock client has a unique lock ID, and the lock implementation uses uniqueCount() to maintain a queue of the proper length.
