# Chapter 11: I/O and TRAP Processing 525

```
exec 4 </dev/tcp/149.4.4.122/80
exec 3>&&
```

d) What do the two exec commands accomplish?
Answer:They open fds 3 and 4 for writing and reading a tcp "socket" connection.

The shell does not let you read and print using the same fd, so the code opens the socket for reading, using fd 4, then copies that fd to fd 3.

e) What are the numbers after /dev/tcp on the first line?
Answer: They are the Internet address (149.4.4.122) and port number (80) that uniquely identify a program running on a computer that is ready to reply to messages that we send to it.

In this case, I've given you the Internet address and port number for the web server running on my computer.

> If your version of ksh is new enough, you may be able to use a "fully qualified domain name" (FQDN) instead of the "dotted-decimal" address shown. In this example, the FQDN is "babbage.cs.ac.edu".

+   f)What sequence of read and print commands must the program at the other end of the TCP/PIP connection in order for these commands to work?

Answer: Because this program first prints one line and then reads as many lines as it get, we can infer that the other program reads a line, then writes one or more lines back to us.

> If you can't get this exercise to work on your computer, go to www.phpptr/phpinteractive/ to see what the interaction should look like. We're not giving away the surprise here!

What we have described is a subset of the Hypertext Transfer Protocol (http). This program is acting as a web browser, which makes an http request (GET /KornShell—be to capitalize it exactly as shown), then reads the server's reply, a series of text lines that the program prints on your screen. In this case, KornShell is the name of a text file in my server's web-page directory.