# Chapter 27: Managing Users, Groups, and Authentication

This command would add the user djf to the admin group and enable that that user to execute any commands using sudo or gksudo.

# # Configuring Kerberos Authentication

Kerberos is a distributed authentication and communication service that was originally developed at the Massachusetts Institute of Technology (MIT). Kerberos provides secure authentication and communication for client/server applications using strong cryptography to enable clients to prove their identity to servers over the network.

Kerberos works by exchanging security information between clients (which can be users or machines), the Kerberos Authentication Server, the resource you are trying to access. The information is initially exchanged when attempting to prove one's identity is known as a ticket. The information used to encrypt tickets and subsequent communications is known as a key. Once the identity of a client is verified, client is granted a Kerberos token that can be used to verify their identity to any Kerberos-aware server. For security reasons, Kerberos tokens are timestamped so that they automatically expire unless renewed by a user or service. The primary system for granting tickets (and holds the master copy of the Kerberos database) is known as the Kerberos Key Distribution Center (KDC).

The timestamps contained within Kerberos tokens (and tickets) can only be verified if the time and data are synchronized across Kerberos clients and servers. Kerberos authentication will fail if client and server clocks skew by more than 5 minutes. You should always run an NTP (Network Time Protocol) daemon on all Kerberos servers and NTP clients on all Kerberos clients to guarantee that their clocks remain in sync.

Kerberos uses the term realm to differentiate between authentication and Internet domains. A Kerberos realm is a set of machines that run on a specific Kerberos server for authentication and, therefore, trust that server. In Kerberos configuration files, your realm is typically identified in uppercase characters in order differentiate it from any similar DNS domain with which it is associated.

MIT's Kerberos implementation is only one of several. Several alternate Kerberos implementations have been created over the years, usually to get around U.S. export restrictions that have been since lifted. This section focuses on vanilla Kerberos from MIT as provided in the Ubuntu repositories.

# # Installing Kerberos Client and Server Commands

Using Kerberos requires that you either build and install it from scratch or that a few basic packages are already installed on your systems. If you need to build yourself, you can download the latest version from http://web.mit.edu/kerberos/www. However,