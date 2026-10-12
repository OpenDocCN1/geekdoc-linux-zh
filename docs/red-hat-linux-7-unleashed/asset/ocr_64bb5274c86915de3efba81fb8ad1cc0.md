undervalue the importance of good networkwide security. It has been reported that over 70% of system compromises originate within the firewall, by disgruntled employees, by curious employees who want to see how systems work, or by competitors' spies.

What is a ssysadmin to do? Use only the console? What about remote sites that are only connected via the Internet?

Enter the Secure Shell, also known as SSH. *SSH* is a suite of programs that allow you to log on to remote servers and transfer files in a secure manner. It is meant to be a replacement for *rlogin*, *rsh*, *telnet*, and *rcp*, which are insecure because they don't encrypt the data they transfer as it moves from one host to another. SSH, on the other hand, scrabbles the data that goes through the network so it is indecipherable to someone using a sniffer. A full discussion of security and encryption technologies is beyond the scope of this book; however, an excellent reference is *Internet Security Professional Reference, Second Edition* (New Riders Publishing, ISBN 1-56205-760-X).

# OpenSSH Debuts with Red Hat Linux 7.0

The new version of Red Hat Linux now includes OpenSSH, a collection of free versions of SSH programs inherited from the kind folks at the OpenBSD Project! The suite includes *ssh*, which replaces *telnet*, the *sshd* daemon, and *scp*, which replaces the *ftp* command. You'll also find other utilities included in the distribution, which is composed primarily of the following .rpm files:

+   openssh-clients-2.1.1p4-1
+   openssh-2.1.1p4-1
+   openssh-askpass-gnome-2.1.1p4-1
+   openssh-server-2.1.1p4-1
+   openssh-askpass-2.1.1p4-1

For more information, browse to http://www.openssh.com/.

With SSH, each host and user has a *private key* and a *public key*. The public key is stored on the server, whereas the private key is kept on the client. Data encrypted with one key can only be decrypted with the other, and vice versa. This means that SSH can be used both for secure communications and for strong authentication, where you need to be sure that the host on the other side of the connection is actually who it claims to be.

Because SSH contains encryption technology, it is illegal to export it from the U.S. *ssh-server* must be installed on the servers (the hosts you are logging on to), *ssh-clients* on the clients (the hosts you are logging on from), and *ssh* on both: *ssh-extras* can be optionally installed on either or both. It is often best to install all packages on all hosts.