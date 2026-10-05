# INTRODUCTION TO OPENSSH

Using public key encryption (page 1111), OpenSSH provides two levels of authentication: server and client/user. The first client verifies that it is connected to the correct server. OpenSSH encrypts communication between the sessions. Once an encrypted connection has been established, OpenSSH makes sure the user is authorized to log in. After verifying the system and user, OpenSSH allows different services to be passed through the connection. These services include interactive shell sessions (ssh), remote command execution (ssh), file copy (scp), FTP services (sftp), X11 client/server communications, and TCP/IP port tunneling.

+   SSH1 versus SSH2 SSH protocol version 2 (SSH2) that offers improved performance, and portability. The two protocols are not compatible. Because SSH1 is being rapidly supplanted by SSH2 and because SSH1 is vulnerable to a man-in-the-middle attack (footnote 3 on page 1114), the client does not support SSH1. Version 2 is floating-point intensive, version 1 does a place on systems without FPUs (floating-point units or accelerators), such as old 486SX systems. As installed, the OpenSSH tools supplied with Ubuntu support SSH2.

+   ssh The ssh allows you to log in to a remote system over a network. You might choose to use a remote system to access a special-purpose application or to take advantage of a device that is available only on that system, or you might use a remote system because it is faster or less busy than the local system. While traveling, many businesspeople use ssh on a laptop to log in on a system at headquarters. From a GUI you can see several simultaneously by logging in on one from a different terminal emulator window.

+   X11 forwarding Once you trust X11 forwarding, it is a simple matter to run an X11 program over ssh from a terminal emulator running on an X11 server and give an X11 command such as xclock; the graphical output appears on the local display. For more information refer to "Forwarding X11" on page 681.

# How OpenSSH Works

When OpenSSH starts, it first establishes an encrypted connection and then authenticates the user. Once these two tasks are completed, OpenSSH allows the two systems to send information back and forth.

OpenSSH uses two key pairs to negotiate an encrypted session: a host key pair and a session key pair. The host key is a set of public/private keys that is established when you install the openssh-server package (page 676). The session key pair is a set of public/private keys that changes hourly.

The first time an OpenSSH client connects with an OpenSSH server, you are asked to verify that it is connected to the correct server (see "First-time authentication" on page 668). After verification, the client makes a copy of the server’s public host