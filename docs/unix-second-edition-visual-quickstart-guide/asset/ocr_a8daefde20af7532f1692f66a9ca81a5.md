# Table 12.1

# Internet Ports and Protocols

| Port | Protocol |
|------|----------|
| 21 | ftp |
| 22 | ssh |
| 23 | telnet |
| 70 | gopher |
| 80 | http |
| 119 | nntp |
| 8080 | http (usually for test servers) |

Protocols are the languages that computers use to communicate with one another. For example, FTP (File Transfer Protocol) is used to transfer files from one computer to another. HTTP (Hypertext Transfer Protocol) is used to transfer data on the World Wide Web.

Ports are like a computer’s ears—they’re “places” that computers listen for connections. Most Web servers run at port 80, and if you connect to http://www.raycomm.com:80/, you’re explicitly saying that you want to talk to the www.raycomm.com computer, at port 80, using HTTP. You could specify a different protocol (FTP, for example) or a different port (8080, for example) to communicate with the same computer in a different way, as Table 12.1 shows.