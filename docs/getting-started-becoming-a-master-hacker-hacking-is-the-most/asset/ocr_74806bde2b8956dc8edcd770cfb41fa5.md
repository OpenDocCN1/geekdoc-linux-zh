stack sets this field as either D or M, don't fragment or more fragments. This is the way that the IP protocol signals to the receiver whether more packet fragments are on the way. If it gets packets with the M flag set, the receiver can hold the packets and reassemble them into a complete packet.

Third, **TTL** or Time to Live. This field indicates how many hops the packet should make before it expires. Windows systems usually have this set to 32 and Linux systems to 64, although it does vary.

Finally, **let's examine window** or window size. This field defines how much buffer the TCP stack has to buffer packets. Remember that one of the beauties of TCP is that it has **“flow control.”** If one side is sending packets too quickly for the other to process, the sender can buffer the packets. Window size defines the size of that buffer. This field alone carries more information about the identity of the sender than any other field in either header. Nearly every operating system has a different window size.

Now that we understand what p0f does, let's put it to work on some packets.