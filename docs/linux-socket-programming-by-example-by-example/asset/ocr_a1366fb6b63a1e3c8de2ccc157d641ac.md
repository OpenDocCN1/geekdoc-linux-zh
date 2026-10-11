It was also noted in the last chapter that connectionless-oriented communication is simpler and more flexible. But you'll see that connection-oriented communication is not really that much more difficult. It does require additional steps, however, and mostly on the server side. A connection is also much more rigid, because after the connection has been established, the socket can only communicate with the connected endpoint.

The selling point in favor of TCP/IP for most application writers is that the communication channel is transparently reliable and that data is delivered in the proper sequence. After the connection has been established, your application can read and write to the socket without worrying about any of the following problems:

+   - Lost packets
+   - Timeouts and retransmissions
+   - Duplicated packets
+   - Packets received out of sequence
+   - Flow control

Like opening a file, your program can

+   1. Establish a TCP/IP connection with a remote socket
+   2. Transmit large amounts of data
+   3. Close the socket

These simple steps are all that is necessary to deliver all of your data safely to the remote end. Proven error recovery software will take care of retrans-mitting lost packets until they can be successfully delivered to the remote host.

# **TCP/IP Handles Lost Packets**

TCP/IP will notice when packets are lost. This does not always happen with UDP. When packet errors are reported, the TCP/IP protocol can immediately respond with retransmissions. However, if an acknowledgement is missing, causing a timeout, the TCP/IP protocol takes steps to ensure that the data is retransmitted to its destination. Carefully crafted algorithms are used to make the transmission of the data nimble, without taxing the network capacity with retransmitted data.