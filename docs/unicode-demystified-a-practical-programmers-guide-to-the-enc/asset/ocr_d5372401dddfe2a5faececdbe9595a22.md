# TTL

Time to live.

+   All DNS records specify how long they are good for, usually up to a week at most. This time is called the record's time to live. When a DNS server or an application stores this record in cache (page 1459), it decrements the TTL value and removes the record from cache when the value reaches zero. A DNS server passes a cached record to another server with the current (decremented) TTL guaranteeing the proper TTL no matter how many servers the record passes through.

+   2. In the IP header, a field that indicates how many more hops should be allowed to make before being discarded or returned.

# TTY

Telepewriter. The terminal device that UNIX was first run from. Today TTY refers to the screen (or window in the case of a terminal emulator), keyboard, and mouse that are connected to a computer. This term appears in UNIX, and GNU/Linux kept the term for the sake of consistency and tradition.

# tunneling

Encapsulation of protocol A packets carried by protocol B, that treats B as though it were a data link layer. Tunneling is used to get data between administrative domains that use a protocol not supported by the internet connecting those domains. See also VPN (page 1501).

# UDP

User Datagram Protocol. The Internet transport layer protocol that provides simple but unreliable data services. UDP is a connectionless protocol that, like TCP (page 1497), is layered on top of IP (page 1474).

Unlike TCP, UDP neither guarantees delivery nor a connection. As a result it is lightweight and efficient, but all error processing and retransmission must be taken care of by the application program. UDP is often used for sending time-sensitive data that is not particularly sensitive to minor loss, such as audio and video data.

# UID

A number that the passwd database associates with a login name.

# undecillion

In the American system 10³⁶ In the British system, this number is named sexillion. See also large number (page 1476).

# Unicast

A packet sent from one host to another. Unicast means one source and one destination.

# unmanaged window

See ignored window on page 1472.