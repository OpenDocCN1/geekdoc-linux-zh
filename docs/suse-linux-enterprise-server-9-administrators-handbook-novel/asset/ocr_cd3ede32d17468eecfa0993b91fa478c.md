# Telnet

In the past, access to computer systems was granted by hard-wiring a terminal device to a server. These devices, commonly known as dumb terminals, would allow for rudimentary character-based access. As systems evolved and networks became more prevalent, this terminal access mode was ported to a network-aware application. The result was called a terminal emulator, and the protocol it used, for the most part, was Telnet.

The Telnet protocol uses TCP port 23 for conversations between the user's system and the target server. When it is invoked and a conversation is established, the user is presented with a username and login prompt. After the user is authenticated, a login shell is created for the user based on information contained in /etc/passwd.

The Telnet service is part of xinetd. You can enable the service by editing /etc/xinetd.d/telnet and changing the disabled flag to no. This is what the Telnet file should look like in a live environment:

```
```text
service telnet
{
        socket_type = stream
        protocol    = tcp
        wait        = no
        user        = root
        server      = /usr/sbin/in.telnetd
        disable     = no
}
```
```

The drawback to the Telnet protocol can be found in the way the packets are sent to the target server. In Telnet, there is no provisioning for protecting the information contained within each packet as it traverses the network. As information is entered in the terminal session, it is broadcasted in cleartext across the network. This includes the original authentication steps, allowing a network eavesdropper to intercept the traffic and collect usernames, passwords, and other sensitive information passed during the conversation. For this reason, the Telnet protocol is considered inappropriate for use.

# ssh

A replacement method for accessing servers can be found in an application called Secure Shell (ssh). This protocol communicates over TCP port 22. This application establishes a link between the host and the destination computer, exchanges a series of cryptographic keys, and establishes an encrypted channel between the two machines. This channel is then used to create a login shell for