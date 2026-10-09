One of the solutions for ensuring packet arrival is to include a unique number. This solution can help packet sequencing. For this to work, the number must be sequential and unique between messages.

If the packet gets out of order, your protocol may hold back higher-numbered packets until the lower-number messages arrive. For example, if packets 1, 2, 4, and 5 arrive, packets 4 and 5 wait until 3 arrives.

Potentially, the network could drop packet 3 during transmission, in which case the receiver could either request packet 3 specifically or acknowledge the packets that arrived. Either way, the sender retransmits the missing message.

# Packet Redundancy

The network may cause mirroring of packets, resulting in duplicates arriving at the destination. The most common cause is when a very late packet arrives after the destination requests a retransmittal. Sequencing eliminates redundant packets. The receiver simply drops the packet with the duplicate sequence ID.

# Verifying Data Integrity

Packets move from source to destination through networks and routers. At any time, the network could corrupt the message (and often does on a congested network). One collision forces the originating hosts to retransmit. In the example above, where packet 3 is lost, the host most likely sent the packet. However, the network could easily have blasted it.

Both UDP and TCP use one's-complement checksums on their data. The IP layer checksums only its own header and ignores the data message. Checksums are useful for detecting minor errors, but it is possible for the errors to cancel each other out. Some networking interfaces include a hardware cyclical redundancy check (CRC) or error correction codes (ECCs) for finding and repairing corrupted data.

Again, packet 3 could actually arrive, but the contents might be corrupted while still passing the IP and UDP checksums.

You could incorporate your own checksum, CRC, hash, or ECC in your packets and messages. Algorithms for these are available on the Internet from the Open Source community. When you choose the validation algorithm, balance it against these items:

+   - The amount of data you're transmitting. Increasing your header size can significantly reduce the network throughput.
- The reparability of your data. Some data may be easily repairable because of redundancy or low criticality.
- Data value versus data position. Checksums are good at quick data value computation, but they lose byte-order significance. A CRC requires more computation but can easily identify bit errors up to the CRC size. For example, a 32-bit CRC can reliably detect bit errors up to 32 bits in length. Beyond 32 bits, it loses reliability.

Data reliability is important for most applications. Checking, validation, and sequencing help ensure safe and orderly arrival of a message. Making sure that the sender and receiver communicate helps smooth the data flow.