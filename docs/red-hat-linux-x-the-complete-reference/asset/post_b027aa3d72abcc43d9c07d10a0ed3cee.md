
You can set up port forwarding to a port on the remote system or to one on your local system. To forward a port on the remote system to a port on your local system, use the ssh -R option, followed by an argument holding the local port, the remote host address, and the remote port to be forwarded, each separated by a colon. This works by allocating a socket to listen to the port on the remote side. Whenever a connection is made to this port, the connection is forwarded over the secure channel, and a connection is made to a remote port from the local machine. In the following example, port 22 on the local system is connected to port 23 on the rabbit.mytrek.com remote system:

```
ssh -R 22:rabbit.mytrek.com:23
```

To forward a port on your local system to a port on a remote system, use the ssh -L option, followed by an argument holding the local port, the remote host address, and the remote port to be forwarded, each separated by a colon. A socket is allocated to listen to the port on the local side. Whenever a connection is made to this port, the connection is forwarded over the secure channel and a connection is made to the remote port on the remote machine. In the following example, port 22 on the local system is connected to port 23 on the rabbit.mytrek.com remote system:

```
ssh -L 22:rabbit.mytrek.com:23
```

You can use the LocalForward and RemoteForward options in your .ssh/config file to set up port forwarding for particular hosts or to specify a default for all hosts you connect to.

## SSH Configuration

The SSH configuration file for each user is in their .ssh/config file. The /etc/ssh/ssh_config file is used to set site-wide defaults. In the configuration file, you can set various options, as listed in the ssh_config man page. The configuration file is designed to specify options for different remote hosts to which you might connect. It is organized into segments, where each segment begins with the keyword HOST, followed by the IP address of the host. The following lines hold the options you have set for that host. A segment ends at the next HOST entry. Of particular interest are the User and Cipher options. Use the User option to specify the names of users on the remote system who are allowed access. With the Cipher option, you can select which encryption method to use for a particular host. Encryption methods include idea, des (standard), triple-des (3des), blowfish (128 bit), arcfour (RSA's RC4), and twofish. The following example allows access from larisa at turtle.mytrek.com and uses Blowfish encryption for transmissions:

```
Host turtle.mytrek.com
    User larisa
    Compression no
    Cipher blowfish
```

To specify global options that apply to any host you connect to, create a HOST entry with the asterisk as its host. HOST *. This entry must be placed at the end of the configuration file because an option is changed only the first time it is set. Any subsequent entries for an option are ignored. Because a host matches on both its own entry and the global one, its specific entry should come before the global entry. The asterisk, *, and the question mark, ?, are both wildcard matching operators that enable you to specify a group of hosts with the same suffix or prefix.

```
Host *
    FallBackToRsh yes
    KeepAlive no
    Cipher idea
```

![](img/32a48d8db4c23e6e2eb70d1e5034c976_402_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abcchm.html

## Kerberos

User authentication can further be controlled for certain services by Kerberos servers, discussed in this chapter. Kerberos authentication provides another level of security whereby individual services can be protected, allowing use of a service only to users who are cleared for access. Kerberos servers are all enabled and configured with authconfig-gtk (Authentication in the System Settings menu or window).

Kerberos is a network authentication protocol that provides encrypted authentication to connections between a client and a server. As an authentication protocol, Kerberos requires a client to prove its identity using encryption methods before it can access a server. Once authenticated, the client and server can conduct all communications using encryption. Whereas firewalls protect only from outside attacks, Kerberos is designed to also protect from attacks from those inside the network. Users already within a network could try to break into local servers. Kerberos places protection around the servers themselves, rather than an entire network or computer. A free version is available from the Massachusetts Institute of Technology at web.mit.edu/kerberos under the MIT Public License, which is similar to the GNU Public License. The name Kerberos comes from Greek mythology and is the name of the three-headed watchdog for Hades. Be sure to check the web.mit.edu/kerberos site for recent upgrades and detailed documentation, including FAQs, manuals, and tutorials.

**Tip** The Kerberos V5 package includes its own versions of network tools such as Telnet, RCP, FTP, and RSH. These provide secure authenticated access by remote users. The tools operate in the same way as their original counterparts described in Chapter 15. The package also contains a Kerberos version of the su administrative login command, ksu.

## Kerberos Servers

The key to Kerberos is a Kerberos server through which all requests for any server services are channeled. The Kerberos server then authenticates a client, identifying the client and validating the client's right to use a particular server. The server maintains a database of authorized users. Kerberos then issues the client an encrypted ticket that the client can use to gain access to the server. For example, if a user needs to check their mail, a request for use of the mail server is sent to the Kerberos server, which then authenticates the user and issues a ticket that is then used to access the mail server. Without a Kerberos-issued ticket, no one can access any of the servers. Originally, this process required that users undergo a separate authentication procedure for each server they wanted to access. However, users now only need to perform an initial authentication that is valid for all servers.

**Tip** On Red Hat, you can use the Kerberos Ticket Manager (Extras Accessories menu) to manage Kerberos tickets, and the authconfig-gtk tool (Authentication in the System Settings window or menu) to specify and enable Kerberos realms.

This process actually involves the use of two servers, an authentication server (AS) and a ticket-granting server (TGS). Together they make up what is known as the key distribution center (KDC). In effect, they distribute keys used to unlock access to services. The authentication server first validates a user's identity. The AS issues a ticket called the ticket-granting ticket (TGT) that allows the user to access the ticket-granting server. The TGS then issues the user another ticket to actually access a service. This way, the user never has any direct access of any kind to a server during the authentication process. The process is somewhat more complex than described. An authenticator using information such as the current time, a checksum, and an optional encryption key is sent along with the ticket and is decrypted with the session key. This authenticator is used by a service to verify your identity.

**Note** You can view your list of current tickets with the klist command.

## Authentication Process

The authentication server validates a user using information in its user database. Each user needs to be registered in the authentication server's database. The database will include a user password and other user information. To access the authentication server, the user provides the username and the password. The password is used to generate a user key with which communication between the AS and the user is encrypted. The user will have their own copy of the user key with which to decrypt communications. The authentication process is illustrated in Figure 18-2.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_404_0.png)

Figure 18-2: Kerberos authentication

Accessing a service with Kerberos involves the following steps:

- 1. The user has to be validated by the authentication server and granted access to the ticket-granting server with a ticket access key. You do this by issuing the `kinit` command, which will ask you to enter your Kerberos username and then send it on to the authentication server (the Kerberos username is usually the same as your username).
- `kinit`
- 2. The AS generates a ticket-granting ticket with which to access the ticket-granting server. This ticket will include a session key that will be used to let you access the TGS. The TGT is sent back to you encrypted with your user key (password).
- 3. The `kinit` program then prompts you to enter your Kerberos password, which it then uses to decrypt the TGT. You can manage your Kerberos password with the `kpasswd` command.
- 4. Now you can use a client program such as a mail client program to access the mail server, for instance. When you do so, the TGT is used to access the TGS, which then will generate a ticket for accessing the mail server. The TGS will generate a new session key for use with just the mail server. This will be provided in the ticket sent to you for accessing the mail server. In effect, there is a TGT session key used for accessing the TGS, and a mail session key used for accessing the mail server. The ticket for the mail server is sent to you encrypted with the TGS session key.
- 5. The client then uses the mail ticket received from the TGS to access the mail server.
- 6. If you want to use another service such as FTP, when your FTP client sends a request to the TGS for a ticket, the TGS will automatically obtain authorization from the authentication server and issue an FTP ticket with an FTP session key. This kind of support remains in effect for a limited period of time, usually several hours, after which you again have to use `kinit` to undergo the authentication process and access the TGS. You can manually destroy any tickets you have with the `kdestroy` command.
