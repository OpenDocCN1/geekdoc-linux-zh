# CHAPTER 7 Transport

# 7.1 Roadmap

This chapter talks about end-to-end transfer of data across IP networks. The Internet provides a number of different transport mechanisms. The most common ones are TCP (Transmission Control Protocol) and UDP (User Datagram Protocol).^1 TCP provides a connection-oriented, reliable, stream-based transport, and UDP an unreliable connectionless datagram-based one. RTP is a newer protocol designed for the transport of real-time streams such as video and audio. In this chapter we will examine the workings of UDP, TCP, and RTP, and their implementations in Linux.

The services transport protocols have to cover a wide range of services, including:

+   - Multiplexing
- Reliability
- Flow control
- Congestion control
- Framing
- Synchronization

> ^1As with most acronyms on the Internet, the abbreviation is more important and well-known the expansion.