The server address and the server address length are the same socket address values that you would have supplied in a call to the sendto(2) function, if you were using UDP. The difference with connection-oriented protocols, however, is that you only establish the destination address *once*. After this function succeeds, all future communications will be with the socket addressed here.

When the function call is successful, the return value is zero. Otherwise, -1 is returned to indicate that an error has occurred, and the nature of the error is recorded in the variable *errno*.

# Preparing to Write the Client Program

To keep the client program short and allow you to focus upon the basic principles, the demonstration program is going to connect to an existing service you have running on your system. The client program will connect to your daytime service to retrieve the current date and time string.

Before the program is presented, however, you should make sure that this service is enabled and operational on your system. As a first step, perform the following:

![](bbox=[0.1, 0.48, 0.49, 0.59])

```
$ grep daytime /etc/services
daytime 13/tcp
daytime 13/udp
$
```

You should see that your system recognizes the daytime Internet service and that it is available on port 13 using tcp. The first line of grep output confirms this for you.

# TIP

> The telnet program can often be used to perform simple tests with TCP/IP servers. It is very important, however, to remember to specify the port number after the IP number (or hostname) on the command line. Otherwise, the port number will default to 23, which is the telnet service!
> 
> To test the daytime service, for example, you must specify the port number 13 after the IP number on the command line.

The next step is to make sure it is operational. The *telnet program* is a program that is often usable for simple tests when *TCP/IP* is used. To test that the daytime service is running, you should be able to perform the following:

![](bbox=[0.1, 0.91, 0.47, 1.0])

```
$ telnet 127.0.0.1 13
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
Tue Aug 17 17:59:30 1999
```