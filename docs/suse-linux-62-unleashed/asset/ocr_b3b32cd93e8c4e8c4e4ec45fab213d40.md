# SMTP and Protocols
CHAPTER 9

# telnet popserver pop-3

where popserver is the name of the machine running the ipop3d program. The pop-3 at
end is where telnet will reference in your /etc/services file for port 110. You should get a
response similar to the following:

```
+OK POP3 popserver.gonzo.gov6.50 server ready
```

This result means the POP server has responded and is awaiting an instruction.
(Typically, this job is transient done by the client mail reader.) If you want to test the
authentication service, to log in as yourself and see whether the server registers your
current email box. For example, to log in as ssh with the password mars1031, enter

# user ssh

```
+OK User name accepted, password please
```

# pass mars1031

```
+OK Mailbox open, 90 messages
```

# quit

```
+OK Sayonara
```

The first line, user, sshah, tells the POP server that the user for whom it will be checking
mail sshah. The response from the server is an acknowledgment that the username sshah
is accepted, and a password is required to access the mailbox. You can then type pass
mars1031, where mars1031 is the password for the sshah user. The server acknowledges
t correct password and username pair with a statement indicating that 90 messages are
currently in user sshah's mail queue. Because you don't want to actually read the mail this
enter quit to terminate the session. The server sends a sign-off message and drops the
connection.

# How APOP Works

By default, the POP server sends all passwords in cleartext (not encrypted). If you're
security-conscious, using cleartext passwords over your network is obviously a bad idea
t tighter control is needed on authentication. This is where APOP support comes.
APOP is a more security-minded way of authenticating users because the passwords are
already encrypted before they're sent over the network.

It works like this: The server issues a challenge to a connecting client. The client appends
t user's password to the challenge then encrypts it using MD5—this is called a hash—and
sends the hash back to the server. The server then compares the client's response with its
 calculated value of the checksum (challenge + user password). If there is a match, the
 client is authenticated and logged on to the POP3 server.

![](bbox=[0.865, 0.611, 0.973, 0.803])