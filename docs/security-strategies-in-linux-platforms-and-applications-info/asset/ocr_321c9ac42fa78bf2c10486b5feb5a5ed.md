# CHAPTER 8 | Networked Filesystems and Remote Access

the expected client commands in their expected directory locations and the actual SSL or Kerberos-enabled client commands. For example, the following commands create soft links between the standard Telnet command and the more secure options described in this section:

```
 # ln -s /usr/bin/telnet-ssl /usr/bin/telnet
# ln -s /usr/kerberos/bin/telnet /usr/bin/telnet
```

You can also make the Telnet server accepts only those connections for which it was designed. The SSL version of Telnet is configured in the internet super server configuration file. For /etc/inetd.conf In that file, you can add the -z secure switch, which accepts only secure connections. If a remote user tries to connect with a regular Telnet client, that person will see the following message before he or she can enter a username or password:

telnet: [SSL required - connection rejected]
Connection closed by foreign host.

In a similar fashion, a Telnet client attempt to connect to a Kerberos server and client options are configured as described earlier in this chapter. Without those settings, a user who attempts to connect to a Kerberos-enabled Telnet server will get the following message before he or she can enter a username or password:

Unencrypted connection refused. Goodbye.
Connection closed by foreign host.

# Remember the Modem

If you have to administer connections from telephone modems, the standard is known as the Remote Authentication Dial In User Service (RADIUS). The open source implementation of this software is based on the work of the FreeRADIUS project, from http://freradius.org/. The implementation of RADIUS is beyond the scope of this book. However, it can be downloaded from the noted Web site, and is also available from standard Ubuntu software repositories.

# The Basics of RADIUS

RADIUS is designed to provide authentication, authorization, and accounting for remote users who want to connect to a network service. In RADIUS documentation, these functions are known as AAA. First, with respect to authentication, different modules allow you to link your authentication directives with the username and password databases of your choice. These databases are used to authenticate users, as well as to set up which remote users are authorized to do. You can set up accounting for the actions of users in various RADIUS configuration files.

![](bbox=[0.915, 0.396, 0.998, 0.633])