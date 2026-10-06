CHAPTER 20 Post Office Protocol and Internet Mail Access Protocol (POP and IMAP) 517

# # Dovecot (IMAP and POP3 Server)

The Dovecot POP3 and IMAP server software is well regarded and is used in many production sites around the Dovecot world. It is a well-tested implementation and readily available in the mainstream Linux distros.

Dovecot provides its IMAP and POP3 functions through the following main processes. Collectively, these processes provide various services that make up the Dovecot ecosystem.

+   - Master process As its name implies, the master process is the primary/overseer process. It is responsible for starting and keeping all the other processes running as needed. It reads the settings/options in the configuration files and exports the values to the other processes. The master process is responsible for collecting and managing all logging information Dovecot generates. The master process runs under the dovecot executable.

+   - Login processes The login processes listen for connection requests for the POP3 and IMAP protocols and implement the minimum handshake protocol requirement before a user logs in successfully. You can find the login processes running under imap-login and pop3-login executables.

+   - Authentication (auth) process Once the processes complete the underlying POP3 or IMAP protocol handshake and setup, control is passed on the appropriate authentication process. The auth process is responsible for performing the actual user authentication (Simple Authentication and Security Layer [SASL] functions) to verify that the user is who she says is. The authentication processes run under a similarly named auth executable.

+   - Mail processes (IMAP, POP3) After authentication is successfully completed, the desired mail process kicks in and provides the user access to mail boxes. The mail process is the actual workhorse that implements the POP3 and IMAP protocol details. The IMAP process runs under an executable called imap, and the POP3 process runs under an executable named pop3.

# # Installing Dovecot

Most Linux distributions have prepackaged binaries for Dovecot in the dist repositories. For example, it can be installed in Fedora/CentOS/RHEL using dnf like so:

```
root@fedora-server ~# dnf -y install dovecot
```

On Debian-like systems, as Ubuntu, Dovecot's IMAP and POP3, functionality is provided in two separate packages: dovecot-imapd and dovecot-pop3d, respectively. They can be installed by using Advanced Packaging Tool (APT) like so:

```
master@ubuntu-server:~# sudo apt-get -y install dovecot-imapd dovecot-pop3d
```