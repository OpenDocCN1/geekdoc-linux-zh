# Using lftp to Access URLs

The original FTP client software was a basic command line, text-oriented client application that offered a simple but efficient interface. Most web browsers offer a graphical interface and can also be used as an FTP client.

Any FTP client allows you to view the directory tree and files. Using ftp as a client is easy. You could use the ftp command to connect to a server such as ftp.redhat.com with the following command:

```
# ftp ftp.redhat.com
```

But that client asks for a username and password. You could enter username anonymous and a random password to access the Red Hat FTP server. But if you accidentally enter a real username and password, that data is sent in clear text, available to anyone who happens to be using the right network analyzer applications on the network. Strangely enough, the ftp command client is not installed on standard RHEL 6 installations.

That's one reason why lftp is better. It automatically attempts an anonymous login, without prompting for a username or password. It also supports command completion, which can especially help you access files and directories with longer names.

Sure, there are risks with most FTP clients, as they transmit data in clear text. But as long as usage of this command is limited to public servers with anonymous access, the risk is minimal. After all, if you use lftp to download Linux packages from public servers, it's not like you're putting any private information at risk. To be sure, there are other security risks with such clients, but Red Hat developers have constantly working to keep that client up to date.

If the risks are acceptable, the lftp command can be used to log in to an FTP server where usernames and passwords are enabled. Those of you studying for the RHCE will set up that kind of very secure FTP (vsFTP) server in. User michael could log in to such a server with the following command:

```
$ lftp ftp.example.org -u michael
```

The lftp client can handle a number of different commands, as shown in Figure 2-20. Some of these commands are described in Table 2-5.