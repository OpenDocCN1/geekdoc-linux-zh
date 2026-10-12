an ephemeral port, and connects this socket to the server’s well-known port. This establishes the connection; you can think of it as joining the two sockets together to make the connection, and indeed a connection is often referred to as a *socket pair* (so a socket is half a connection).

For details of sockets and programming with TCP/IP see the sublime book:

+   Stevens UNIX Network Programming (1990, Prentice Hall, PTR)

While this is a programming text, it gives a lot of useful insights into how TCP/IP works, especially how clients and servers interact.

# telnet

In the early days of the Internet, **telnet** and **ftp** (Module 17.2) made up almost all the traffic on the Internet. By the mid-1990s, this had dropped to about 40% and now it makes up 10% or less, and is still dropping rapidly. This reflects the growth in e-mail, Web and multi-media applications.

The Windows NT Server 4.0 Resource Kit contains a **telnet** server, as does Windows-2000.

**telnet** has a huge number of special options, which nowadays don’t seem very interesting. See Stevens, Chapter 26, or the **telnet** (1) manpage on a Linux or UNIX system.

Because **telnet** normally sends to the remote system everything you type – including control characters – you need a special way to send commands to **telnet** itself. On Windows the window menus let you do this. On Linux, **telnet** has an “escape character,” which is usually Ctrl-]. When you type this, **telnet** gives you its own prompt, and treats the next line you type as an instruction to **telnet**, not something to send to the remote machine. We rarely use this for anything except to quit. For more information, type Ctrl-] in a **telnet** session and enter “help”.

You can start the **telnet** client manually from the command line, or in your Web browser enter the URL `“telnet://machinename`.”

# telnet-related programs

The program **netcat** (also known as **nc**, Module 17.4) is like a trimmed-down version of **telnet** – it doesn’t have any of **telnet**’s fancy options – but in other ways it is much more flexible and is ideal for testing network services.

The **rsh**, **rcp**, and **rlogin** are functionally related to **telnet** although they don’t use the **telnet** protocol. These are collectively known as the “r-commands” (“r” for remote) and originated in the Berkeley (BSD) version of UNIX, where a lot of TCP/IP was developed and networking was made practical for day-to-day use.

**rsh** (remote shell) and **r exec** (remote execute) let you execute a single command on a remote system. For example,

```
rsh bob date
what time does Bob say it is?
```

**rcp** (remote copy) copies a file between the locate and a remote system. For example,

```
rcp bob:/tmp/abc.txt mine.txt
copies a file from Bob
```

**rlogin** (remote login) lets you logon to a remote system without having to enter your username and password.