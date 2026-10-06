# CHAPTER 20 Post Office Protocol and Internet Mail Access Protocol (POP and IMAP)

# Checking Basic POP3 Functionality

If everything has worked correctly, you should now have a running IMAP server and POP3 server. The next logical step is to test the services for actual functionality.

We begin by using Telnet to connect to the POP3 server (localhost in this example). From a command prompt, type the following:

```
[root@server ~]# telnet localhost 110
Trying ..
Connected to localhost.
Escape character is '^]'.
OK Dovecot ready.
```

The server is now waiting for you to give it a command (Don't worry that you don't see a prompt.) Start by submitting your login name as follows:

USER login

Here, yourlogin, is of course, your login ID. The server responds with this:

+OK User name accepted, password please

Now tell your password using the PASS command:

PASS password

Here, yourpassword is your password. The server responds with this:

+OK logged in.

You're now logged in and can issue commands to read your mail. Since you are simply validating that the server is working, you can log out. Simply type QUIT, and the server will close the connection:

QUIT

+OK Logging out.
Connection closed by foreign host.

That's it.

# Checking Basic IMAP Functionality

We will use Telnet to connect to the IMAP server (localhost in this example) and test it for basic IMAP functionality. From the command prompt, type the following:

```
[root@server ~]# telnet localhost 143
```