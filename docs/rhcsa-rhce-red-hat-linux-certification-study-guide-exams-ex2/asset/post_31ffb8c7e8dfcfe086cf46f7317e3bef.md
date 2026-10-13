
## LAB ANSWERS

For most of these labs, you may be using an e-mail client like mutt. To send an e-mail to user michael@localhost, take the following steps:

- 1. Run the mutt michael@localhost command. The To: michael@localhost message should appear.
- 2. Press ENTER. At the Subject: prompt, enter an appropriate test subject name and press ENTER.
- 3. You're taken to a blank screen in the vi editor. Use commands appropriate to that editor to a screen similar to that shown in Figure 13-5.
- 4. From the screen shown in Figure 13-5, press y to send the noted message.

In addition, you may be verifying e-mail receipt in files named by username in the /var/spool/mail directory. Normally, such e-mail can be reviewed from within a user account with the mail command. In addition, you may be verifying access to a running SMTP server with the telnet ip_address 25 command, where ip_address is the IP address of the SMTP server.

After making a configuration change, don't forget to process the file appropriately. For Postfix, the postmap filename command processes the file. For sendmail, the /etc/mail/make script processes the file. For the common /etc/aliases file, the newaliases command processes the file. And don't forget to make sure the service actually re-reads the new configuration files.

### Lab 1

In Postfix, to disable local-only access in the /etc/postfix/main.cf file, change the inet_interfaces directive to accept all connections:

```
inet_interfaces = all
```

FIGURE 13-5

The mutt e-mail client.

![](img/9139201cfcaf4292284a0eed074928e5_755_0.png)

But to meet the requirements of the lab, you'll want to retain the default value of that directive:

```
inet_interfaces = localhost
```

Make sure Postfix is active (and any alternative mail servers such as sendmail are not). In general, to verify authentication on an SMTP server, connect from the local system with the telnet localhost 25 command. When you see a message similar to

```
220 maui.example.com ESMTP Postfix
```

type in the following command:

```
EHLO localhost
```

Depending on the configuration, you should see messages similar to the following:

```
250-AUTH LOGIN PLAIN
250-AUTH=LOGIN PLAIN
```

To verify receipt of e-mail in a user account, log in to that account, or at least verify the time stamp associated with the username in the /var/mail directory. To make sure e-mail directed to the root user is redirected to a regular user account, you'd add a line like the following to the /etc/aliases file:

```
root: michael
```

Given the wording for the question, any standard user account would be acceptable. Of course, to implement this change, you'll have to run the newaliases command, which processes this file into the /etc/aliases.db file.

To make this work, you'll want to use a command line client such as mutt or even mail as defined in Chapter 2. For example, if you send a test e-mail to the local root user, the message should be received by user michael (or whomever is configured in the /etc/aliases file to receive e-mail forwarded from the root user).

### Lab 2

To enable access from more than just the localhost, you'll need to modify the inet_interfaces directive in /etc/postfix/main.cf to

```
inet_interfaces = all
```

The next job is to limit access to a specific network, in this case, example.com. While there are options in /etc/postfix files, perhaps the most efficient way to limit access to a specific network is with an appropriate iptables-based firewall rule. For example, the following custom rule would limit access to TCP port 25 to systems on the given IP address network. The network shown is based on the originally defined configuration for example.com, the 192.168.122.0/24 network:

```
-A INPUT -m state --state NEW -m tcp -p tcp -s 192.168.122.0/24 --dport 25 -j ACCEPT
```

In addition, you'll need to set up this network in the /etc/postfix/access file with a rule like the following:

```
192.168.122 OK
```

Once Postfix is running, you should be able to confirm the result with an appropriate telnet command from a remote system. For example, if Postfix is configured on a system with a 192.168.122.50 IP address, the command would be

```
# telnet 192.168.122.50 25
```

The configuration of a smart host in Postfix is based on the relayhost directive. For the parameters given in the Lab, if the physical host is located on system maui.example.com, the directive in the main.cf file would be

```
relayhost = maui.example.com
```

If Postfix on the server r.example.com system is properly configured as a smart host, e-mails to the forwarded host should be reliably delivered, and even logged in the appropriate /var/log/maillog file.

### Lab 3

With the iptables rule shown in Lab 2, access should already be prohibited from other networks. However, if you did not include the 192.168.122.0/24 network address in the iptables rule shown in the answer to Lab 2, a different approach is available. You can use options available in the /etc/postfix/access file, such as the following to reject messages from the example.org network. If your example.org network uses a different IP address, revise accordingly.

```
192.168.100 REJECT
```

It should be easy to verify connections to the SMTP server from a remote system. From prohibited networks, when you run a command like: telnet 192.168.122.50 25 from a host on the 192.168.100.0/24 network, you should see the following output:

```
Trying 192.168.122.50...

telnet: connect to address 192.168.122.50: No route to host
```

### Lab 4

This lab should be straightforward. As long as sendmail and sendmail-cf are installed on the local system, the basic steps to make the move from Postfix to sendmail are as follows:

- 1. Stop the Postfix service with a command like `/etc/init.d/postfix stop`.
- 2. Run the alternatives `--config mta` script, and select sendmail.

### Lab 5

IPv6 networking is not enabled on some systems. But when it is, open the sendmail.mc file in the /etc/mail directory. To configure sendmail to accept connections from both IPv4 and IPv6 addresses, first disable the following directive. The added dnl in front turns it into a comment.

```
dnl DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

Next, to let sendmail listen for both IPv4 and IPv6 traffic, activate the following directive:

```
DAEMON_OPTIONS(`Name=MTA-v4, Family=inet, Name=MTA-v6, Family=inet6')
```

If successful, you should be able to connect to the system with either of the following commands:

```
# telnet ::1 25
# telnet 127.0.0.1 25
```

Forwarding from the root account can be enabled through the /etc/aliases file, as explained in the answer to Lab 1.

### Lab 6

In sendmail, to disable local-only access in the /etc/mail/sendmail.mc file, comment out the following line. Unlike in most Linux configuration files, the comment code is a dnl at the start of this line:

```
DAEMON_OPTIONS(`Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

The dnl at the end of the line does not affect the command to its left.

Next, you'll want to enable support through /etc/mail/access. To allow access to the example.com network as discussed in this book, add the following line to that file:

```
192.168.122 RELAY
```

For this lab, assume the sendmail system is on server1.example.com, with IP address 192.168.122.50, and the physical system is on maui.example.com on IP address 192.168.122.1. Return to the sendmail.mc file, and then look at this directive:

```
dnl define(`SMART_HOST', `smtp.your.provider')dnl
```

Based on the conditions given, you'd change that directive to

```
define(`SMART_HOST', `maui.example.com')dnl
```

### Lab 7

This lab is quite similar to Lab 2. While there are options in the sendmail configuration files, the most efficient way to limit access to a specific network is still with an appropriate iptables-based firewall rule. The rule discussed in the answer to Lab 2 would also work in this case. Alternatively, you can configure access limits in the /etc/mail/access file, such as

```
Connect: 192.168.122 OK
Connect: 192.168.100 REJECT
```
