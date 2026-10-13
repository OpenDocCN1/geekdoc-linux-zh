# The master.cf Configuration File

Generally, you should not have to make changes to the master.cf file. It's configured to set up Postfix for regular SMTP services. As shown in the first page of the file, it does include options for the submission protocol on port 587, which is required for a smart host relay to some ISP's e-mail servers. It also supports the configuration of secure SMTP.

# Test the Current Postfix Configuration

As noted in previous chapters, the telnet command is an excellent way to review the current status of a service on a local system. Based on the default configuration of Postfix, an active version of this service should be listening on port 25. In that case, a telnet localhost 25 command should return messages similar to the following:

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 Maui.example.com ESMTP Postfix
```

If IPv6 networking is enabled on the local system, the IPv4 loopback address (127.0.0.1) would be replaced by the regular IPv6 loopback address (::1). The quit command can be used to exit from this connection. But don't quit yet. The EHLO localhost command is important; the EHLO is the enhanced HELO command, which introduces the basic parameters of an SMTP server.

```
EHLO localhost
250-maui.example.com
250-PIPELINING
250-SIZE 10240000
250-VRFY
250-ETRN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250 DSN
```

For our purposes, the most important information is what's missing. No authentication is required on this server. When authentication is properly configured on Postfix, you'll also see the following line in the output:

```
250-AUTH GSSAPI
```