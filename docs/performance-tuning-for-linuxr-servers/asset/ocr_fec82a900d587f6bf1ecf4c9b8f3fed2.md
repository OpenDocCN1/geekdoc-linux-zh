![](bbox=[0.184, 0.095, 0.787, 0.49])

The first three packets illustrate the TCP three-way handshake used to establish a connection to the web server. The fourth packet contains the HTTP request from the client, and the sixth contains the response header with the 200 OK message. The remaining packets are mostly either data packets containing the body of the HTTP response (packets from the server to the client) or the TCP acknowledgments for that data (packets from the client to the server). The final four packets are the four-way handshake used to shut down the connection (the first FIN from the server is packet number 30; the FIN bit is not visible in the figure but it is there if you expand the view of the packet).

Figure 15-2 illustrates one packet in detail.

# **Figure 15-2.** Detail of one packet exchange captured by the Ethereal tool.

[View full size image]