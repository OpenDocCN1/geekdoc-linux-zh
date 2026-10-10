# Service: tftp

**Hacker's Strategy:** Often used to load Internetworking Operating Systems (IOS) into various routers and switches, port 69 Trivial File Transfer Protocol (tftp) services operate as a less complicated form of FTP. In a nutshell, tftp is a very simple protocol used to transfer files. tftp is also designed to fit into read-only memory, and is used during the bootstrap process of diskless systems. tftp packets have no provision for authentication; because tftp was designed for use during the bootstrap process, it was impossible to provide a username and password. With these glitches in numerous variations of daemons, simple techniques have made it possible for anyone on the Internet to retrieve copies of world-readable files, such as /etc/passwd (password files), for decryption.

![](bbox=[0.12, 0.27, 0.61, 0.47])

**Figure 4.6** Output from a successful finger query.

# Port: 79

# Service: finger

**Hacker's Strategy:** When an email account is “fingered,” it returns useful discovery information about that account. Although the information returned varies from daemon to daemon and account to account, on some systems, finger reports whether the user is currently in session. Other systems return information including the user's full name, address, and/or telephone number. The finger process is relatively simple: A finger client issues an active open to this port, and sends a one-line query with login data. The server processes the query, returns the output, and closes the connection. The output received from port 79 is considered highly sensitive, as it can reveal detailed information on users. Sample output from the Discovery: finger phase of an analysis is shown in Figure 4.6. The actual data is masked for user anonymity.

# Port: 80

# Service: http

**Hacker's Strategy:** An acronym for the Hypertext Transfer Protocol, HTTP is the underlying protocol for the Internet's World Wide Web. The protocol defines how messages are formatted and transmitted, and operates as a stateless protocol because each command is executed independently, without any knowledge of the previous commands. The best example of this daemon in action occurs when a Web site address (URL) is entered in a browser. Underneath, this actually sends an HTTP command to a Web server, directing it to serve or transmit the requested Web page to the Web browser. The primary vulnerability with specific variations of this daemon is the Web page hack. An