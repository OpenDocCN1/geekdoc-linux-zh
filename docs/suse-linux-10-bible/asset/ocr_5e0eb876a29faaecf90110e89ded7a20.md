# Chapter 17 + Mail Servers – Postfix, Sendmail, Qpopper, and Cyrus 487

```
# pop2 stream tcp await root /usr/sbin/tcpd ipop2d
# pop3 stream tcp await root /usr/sbin/tcpd ipop3d
# pop3 stream tcp await root /usr/sbin/tcpd ipop3d
pop3 stream tcp await root /usr/sbin/tcpd /usr/sbin/qpopper -s
#
```

The network process inetd accepts connections from standard ports and passes control over a specific application. Whereas Postfix listens on port 25 in daemon mode, Qpopper relies on inetd to provide its listening services.

When started, inetd to enable POP3 access to your mail.

```
bible:- # rinetd start
dne
```

Once started, you can test connectivity with Telnet as we discuss in more detail in Chapter 15. Listing 17-4 shows an example.

# Listing 17-4: Testing the POP3 Server with Telnet

```
bible:- # telnet localhost 110
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'
+OK ready <<2282.1088970620@bible>
user
+OK Password required for just.
pass password
+OK just has 1 visible message (0 hidden) in 544 octets.
```

As you can see, the user just has one unread mail that is 544 octets in.

You can pass other parameters to Qpopper to extend its functionality. For example, if you want to allow users to enter their usernames in uppercase or mixed case, you can add -c to the Qpopper command line in inetd.conf to enable this. Another common parameter is -R to disable reverse name lookups (so that the host name and not the IP address is stored in the system log).

If you want to store your Qpopper options in a configuration file instead of specifying them on the command line through inetd.conf, you need to call Qpopper with the -f parameter (to set the configuration file):

# Pop et al
#