
feature-free, code:

```
event message_t* Receive.receive(message_t* msg, void* payload, uint8_t len) {
    return msg;
}
```

A receive handler can always copy needed data out of the packet and just return the passed buffer. There are, however, situations when this is undesirable. One common example is a routing queue. If the node has to forward the packet it just received, then copying it into another buffer is wasteful. Instead, a queue allocates a bunch of packets, and in addition to a send queue, keeps a free list. When the routing layer receives a packet to forward, it sees if there are any packets left in the free list. If so, it puts the received packet into the send queue and returns a packet from the free list, giving the radio stack a buffer to receive the next packet into. If there are no packets left in the free list, then the queue can’t accept the packet and so just returns it back to the radio for re-use. The pseudocode looks something like this:

```
receive (m):
    if I’m not the next hop, return m  // Not for me
    if my free list is empty, return m // No space
    else
        put m on forwarding queue
        return entry from free list
```

One of the most common mistakes early TinyOS programmers encounter is misusing the Receive interface. For example, imagine a protocol that does this:

```
event message_t* LowerReceive.receive(message_t* m, void* payload, uint8_t len) {
    processPacket(m);
    if (amDestination(m)) {
        signal UpperReceive.receive(m, payload, len);
    }
    return m;
}
```

The problem with this code is that it ignores the return value from the signal to UpperReceive.receive. If the component that handles this event performs a buffer swap – e.g. it has a forwarding queue – then the packet it returns is lost. Furthermore, the packet that it has put on the queue has also been returned to the radio for the next packet reception. This means that, when the packet reaches the end of the queue, the node may send something completely different than what it decided to forward (e.g. a packet for a completely different protocol).

Note, however, that using enum types in variable declarations can waste memory, as enums default to integer width. For example, imagine this enum:

```
typedef enum {
  STATE_OFF = 0,
  STATE_STARTING = 1,
  STATE_ON = 2,
  STATE_STOPPING = 3
} state_t;
```

Here are two different ways you might allocate the state variable in question:

```
state_t state; // platform int size (e.g., 2-4 bytes)
uint8_t state; // one byte
```

Even though the valid range is 0–3, the former will allocate a native integer, which on a microcontroller is usually 2 bytes, but could be 4 bytes on low-power microprocessors. The second will allocate a single byte. So you should use enums to declare constants, but avoid declaring variables of an enum type.

> Programming Hint 5 CONSERVE MEMORY BY USING ENUMS RATHER THAN CONST VARIABLES FOR INTEGER CONSTANTS, AND DON'T DECLARE VARIABLES WITH AN ENUM TYPE.

## 3.5.3 Platform-independent types

To simplify networking code, TinyOS has traditionally used structs to define message formats and directly access messages – this avoids the programming complexity and overheads of using marshalling and unmarshalling functions to convert between host and network message representations. For example, the standard header of a packet for the CC2420 802.15.4 wireless radio chip² looks something like this:

```
typedef struct cc2420_header_t {
  uint8_t length;
  uint16_t fcf;
  uint8_t dsn;
  uint16_t destpan;
  uint16_t dest;
  uint16_t src;
  uint8_t type;
} cc2420_header_t;
```

Listing 3.30 CC2420 packet header

That is, it has a 1-byte length field, a 2-byte frame control field, a 1-byte sequence number, a 2-byte group, a 2-byte destination, a 2-byte source, and 1-byte type fields. Defining this as a structure allows you to easily access the fields, allocate storage, etc.

² Standard in that IEEE 802.15.4 has several options, such as 0-byte, 2-byte, or 8-byte addressing, and so this is just the format TinyOS uses by default.
