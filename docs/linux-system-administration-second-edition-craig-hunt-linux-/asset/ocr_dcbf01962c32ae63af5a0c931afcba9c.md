# Chapter 12: TCP/IP Linux Networking

# Overview

Perhaps more than any other computer technology, networking has changed our lives. Today it's possible to shop, read newspapers, obtain music and software, do research, correspond with colleagues, and even earn a living entirely online. Although there are costs associated with this new use for computers, society as a whole is rapidly embracing the Internet.

Today's networking protocols began life on Unix systems. At the core of the Internet (and of most local networks) lies a protocol known as the *Transmission Control Protocol/Internet Protocol (TCP/IP)*. TCP/IP was first developed on what are by today's standards primitive versions of Unix. As a clone of Unix, Linux has a tightly knit set of TCP/IP networking tools. Indeed, many of Linux's networking tools are the same as those used on "traditional" Unix systems.

This chapter introduces TCP/IP networking in Linux. It begins with an overview of the design of TCP/IP and then launches into the details of TCP/IP configuration in Linux. One very common use of TCP/IP networking is to provide file and printer sharing on a small network, so that users of one system can directly use files and printers on another. This chapter therefore describes this use, although only in broad strokes. TCP/IP is also used for providing many Internet services, such as Web and FTP servers, so these topics are touched upon. Two other chapters in this book (13 and 14) cover additional TCP/IP topics: The X Window System and mail servers.

# Understanding TCP/IP Networking

Chances are you're familiar with how network tools function, at least from the user's point of view. As with so many aspects of our world, however, there's considerable complexity hidden beneath the surface of common network tools like e-mail and remote printing. Understanding the basic design of TCP/IP networking can be invaluable when you're configuring a system to use these features—and particularly when troubleshooting TCP/IP problems. This section therefore presents an overview of critical design features of TCP/IP and of computer networking in general. If you are already familiar with these concepts, feel free to begin with the "TCP/IP Configuration" section instead.

# Network Stacks

The basic goal of networking, from the point of view of high-level software, is to transfer information from a specific program running on one computer to a specific program running on another computer. For instance, when you run a Web browser such as Netscape, the goal is to transmit a request for specific documents from Netscape Navigator to a Web server program (such as Apache) on a remote computer. Apache responds by returning one or more documents to Navigator. This process of exchanges may repeat many times.

**Note** The term *server* has two meanings. First, it can refer to a *program* that runs on a computer. Apache is a Web server, for example. Second, it can mean the *computer* that runs a server program. Likewise, *client* can refer to either a program that requests information of a server program or a computer that requests information of a server computer. When these terms are applied to entire computers, confusion can quickly result in some environments because a single computer can function as both client and server simultaneously.