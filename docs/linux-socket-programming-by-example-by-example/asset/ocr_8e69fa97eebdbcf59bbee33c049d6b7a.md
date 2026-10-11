```
@pepper
$ telnet 192.168.0.1 9099
Trying 192.168.0.1...
Connected to 192.168.0.1.
Escape character is '^]'.
Sunday Aug 22 21:40:27 1999
Connection closed by foreign host.
@pepper
$
```

The session shown demonstrates the following:

+   1. The first command in the session output shows the server being started on **pepper** with a wild server address (but also using the default port number of **9099**).
+   2. The telnet to address 127.0.0.1 port **9099** provoked a response successfully from our server. This contact was made with the server using the local loopback interface.
+   3. The telnet to address 192.168.0.1 port **9099** also provoked a successful response from our server. This proved that the server could be reached from yet a different IP address.

As further proof of the wild nature of the server address, you can try contacting the server from another host. The following shows a connect attempt from host **slug**:

![](bbox=[0.07, 0.56, 0.18, 0.65])

```
@slug
$ telnet 192.168.0.1 9099
Trying 192.168.0.1...
Connected to 192.168.0.1.
Escape character is '^]'.
Sunday Aug 22 21:47:52 1999
Connection closed by foreign host.
@slug
$
```

The telnet command used on host **slug** still contacts the server on interface address 192.168.0.1 in this example. This proves that the connection attempt went through the network card via the Ethernet link and was able to contact the server. Had the server address been bound only to 127.0.0.1, host **slug** would not be able to reach the server on **pepper**.

# **Modifying the Client Program**

To provide a more convincing demonstration, you will dispense with the telnet command. Instead, the client program from the previous chapter will be used with a few modifications applied. Listing 8.2 shows the modified client program.