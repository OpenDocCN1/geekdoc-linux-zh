# 7.7 RTP–Real-Time Protocol

The RTP-time protocol is designed to carry multimedia flows over the Internet. Whether RTP is a transport layer protocol or an application layer protocol is a commonly debated point. For the argument that RTP is an application layer protocol are the facts that RTP data packets are carried in UDP segments (a transport layer service), and RTP is usually implemented in user space. For the contrary argument is the fact that RTP provides a number of additional services to application layer layer these are synchronization and framing. RFC 1889 describes RTP and a number of other RFCs describe different payload formats for particular media types. RTP is generally implemented as a user library and not in the kernel, so is is beyond the scope of this work.

# 7.8 Writing a New Transport Layer

If you are developing a new transport layer that uses IP as its networking layer and sockets as the application API, then linking it with the existing protocol suites becomes simply a matter of writing the appropriate linkage functions and filling in the function holding structures (see Section 7.3.4).

# 7.9 Summary

This chapter examined transport protocols and their implementation. The facilities provided by the transport layer, that is, multiplexing, reliability, flow and congestion control, synchronization, and framing, each have been examined and their implementations detailed. A comparison of popular transport protocols TCP, UDP, and RTP, has been made and instructions on writing your own transport layer given.