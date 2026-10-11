# Datagram Vulnerability

There is vulnerability in this wrapper design for datagram servers. Did you spot the problem? Hint: It has to do with the server looping.

Datagram servers that loop, as in the one shown, have a vulnerability to attack, using the wrapper concept. When no server process is running, the wrapper program is always able to screen the datagram before the server reads it. However, if the server waits for more datagrams and exits only after it times out, the wrapper program is not used to screen out those extra datagrams. This exposure can be summarized as follows:

+   1. A datagram arrives, alerting inetd.
+   2. The inetd daemon starts the wrapper program.
+   3. The wrapper program allows the datagram, and calls *exec*(2) to start the datagram server.
+   4. The datagram server reads and processes the datagram.
+   5. The server waits for another datagram.
+   6. If a datagram arrives, then step 4 is repeated.
+   7. Otherwise, the server times out and exits.
+   8. Repeat step 1.

While the server continues to run, the process repeats at step 4. This leaves out the security check in step 3. If you are quick enough, you can demonstrate this for yourself with the example programs provided earlier.

For better security, you have only a few options:

+   - Use only *nowait*-styled datagram servers (these servers process one datagram and exit). This forces all requests to be scrutinized by the wrapper program.
+   
+   - Use custom code within your datagram server to test each datagram before it is accepted for processing.

A compromise method is to run shorter timeout periods, but this still leaves some exposure.

For these reasons, many sites will choose to disable the datagram service if a TCP version of the same service exists (the TCP request is always checked by the wrapper program). Where the datagram service must be offered, secure sites will not allow their datagram servers to loop. This requires source code changes to the server or a custom server program is written instead. Alternatively, the server program itself checks every access of the requesting client and does not rely on the TCP wrapper concept for this.