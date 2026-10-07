# Understanding TCP/IP Networking

Chances are, you're familiar with how network tools function, at least from the user's
point of view. As with so many aspects of our world, however, there's considerable com-
plexity hidden behind the surface of common network tools like e-mail and remote
printing. Using the basic design of TCP/IP networking can be invaluable when
you're configuring a system to use these features—and particularly when troubleshooting
TCP/IP problems. This section therefore presents an overview of critical design features
of TCP/IP and of computer networking in general. If you are already familiar with these
concepts, feel free to begin with the “TCP/IP Configuration” section inside.

# Network Stacks

The basic goal of networking, from the point of view of high-level software, is to transfer
information from a specific program running on one computer to a specific program run-
ing another computer. For instance, when you run a Web browser as Netscape,
t goal is to transmit request for specific documents from Netscape Navigator to a Web
server program (such as Apache) on a remote computer. Apache responds by returning
one or more documents to Navigator. This process of exchanges can repeat many times.

> NOTE The term server has two meanings. First, it can refer to a program that
runs on a computer. Apache is a Web server, for example. Second, it can mean
t computer that runs a server program. Likewise, client can refer to either a pro-
gram that requests information of a server program or a computer that requests
information of a server computer. When these terms are applied to entire com-
put, fusion can quickly result in some environments because a single com-
puter can function as both client and server simultaneously.

One of the problems encountered in achieving the goal of data exchange between pro-ams is in controlling access to the network. If programs like Netscape were allowed to
control the network hardware directly, chaos would soon ensue, as programs would
interfere with one another. At the core of the solution to this problem lies the concept of
a network stack. This is a set of small software modules, functioning in series, each of
which interfaces with two others (or with one other and the network hardware or a
human). Network applications—both clients and servers—lie at the top of the network
stack. These applications communicate with the layer below them, and so until the
bottom layer is reached, at which point the data leave the computer and traverse the net-
work to the destination system. At that point, the process is reversed, and data travel up
the stack to the destination application. This application can then send a reply via the
same method. Figure 15.1 illustrates this process.