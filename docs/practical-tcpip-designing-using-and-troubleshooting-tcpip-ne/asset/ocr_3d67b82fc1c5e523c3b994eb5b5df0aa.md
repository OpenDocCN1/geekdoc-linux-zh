# Part 3

# Microsoft Windows Networking on a TCP/IP network

# Introduction

Most real-world networks contain Microsoft Windows machines, and increasingly they contain Linux and UNIX machines too. Windows Networking is very different to the TCP/IP networking we've covered so far. It was developed separately and uses its own protocols and mechanisms, layered on top of and separate from TCP/IP, for much of its basic operation, including:

+   1. name resolution
+   2. logon and user authentication
+   3. “browsing” the network to automatically find lists of available machines and resources.

The challenge is to make these two very different worlds operate well on the same network, and to apply to Windows Networking the same investigative and diagnostic approach we've used for everything else.

In the five chapters in this part of the book, we give an overview of the major architectural features of Windows Networking, then cover in detail name resolution, authentication, and browsing, and finish off with a brief chapter on using Windows Networking in practice.

![](bbox=[0.97, 0.45, 1.0, 0.59])