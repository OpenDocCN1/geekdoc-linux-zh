# 202 Lesson 18

In this chapter, we talk about how Unix is used in the networking areas of remote access and what security implications may arise from doing so.

With the proper configuration, you could spread Unix machines around the globe and at each your user environment, files, and programs would appear all just as you do at home. This is the beauty and power of networking. Let's begin with using telnet.

# Using telnet

Using telnet is not only very common, but also a simple to use terminal program. It is invoked by the telnet command on just about every operating system known to man that is running the TCP/IP protocol. TCP/IP is a protocol suite that allows telnet (and most of the rest of the utilities in this lesson) to function in the first place. TCP/IP is beyond the scope of this book, but you should be familiar with what an IP address is if you are going to enter it in the next example. As well, it will be noted that whenever you, use ssh, which stands for secure shell. This protocol will provide you with encryption that can be used to secure a connection you would have normally made with the simple telnet program, which is not normally secure. Despite however insecure it is, there is still a large number of people out there that use telnet all the time.

Telnet's primary use, it enables you to open a login session on a remote machine. To use the telnet command, issue the command as follows: telnet <remote machine>, where <remote machine> is either an IP address or a hostname. You will be prompted with login and password prompt as if you were sitting at the console of the remote machine. From here, follow the lessons learned in Lesson 1, “Getting Started,” and you will be able to log in and use your Unix system remotely.

```
> telnet 10.1.1.1
telnet pri
```

In the last two examples, you can see that it is easy to telnet to a host. You need only to add the hostname or IP address after the telnet command, and the system will attempt to establish a connection (and telnet session) with the machine you specify. Make sure you master this skill; you will be doing this frequently if you use Unix often.