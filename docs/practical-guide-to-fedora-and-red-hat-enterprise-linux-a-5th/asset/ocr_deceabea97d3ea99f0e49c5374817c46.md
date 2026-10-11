```
# by default we allow relaying from localhost....
Connect:localhost.localhostdomain                RELAY
Connect:localhost                                 RELAY
Connect:127.0.0.1                                 RELAY
```

You can add systems to the list in **access** by adding an IP address followed by white-space and the word **RELAY**. The following line adds the 192.168. subnet to the list of hosts that the local system relays mail for:

```
Connect:192.168.                                    RELAY
```

The **sendmail** init script regenerates **access.db** from **access** each time you run it, as when you restart **sendmail**.

# virtusertable: Serves Email to Multiple Domains

When the DNS **MX** records are set up properly, a single system can serve email to multiple domains. On a system that serves mail to many domains, you need a way to sort the incoming mail so that it goes to the right places. The **virtusertable** file can forward inbound email addressed to different domains (aliases cannot do this).

As **sendmail** is configured by Fedora/RHEL, **virtusertable** is enabled. You need to put forwarding instructions in the **/etc/mail/virtusertable** file and restart **sendmail** to serve the specified domains. The **virtusertable** file is similar to the **aliases** file (page 675), except the left column contains full email addresses, not just local ones. Each line in **virtusertable** starts with the address that the email was sent to, followed by whitespace and the address **sendmail** will forward the email to. As with **aliases**, the destination can be a local user, an email address, a file, or a pipe symbol (|), followed by a command.

The following line from **virtusertable** forwards mail addressed to **zach@tccorp.com** to **zcs**, a local user:

```
zach@tccorp.com                                   zcs
```

You can also forward email for a user to a remote email address:

```
sams@bravo.com                                   sams@tccorp.com
```

You can forward all email destined for a domain to another domain without specifying each user individually. To forward mail for every user at **bravo.com** to **tccorp.com**, specify **@bravo.com** as the first address on the line. When **sendmail** forwards email, it replaces the **%1** in the destination address with the name of the recipient. The next line forwards all email addressed to **bravo.com** to **tccorp.com**, keeping the original recipients' names:

```
@bravo.com                                       @%1@tccorp.com
```

Finally you can specify that email intended for a specific user should be rejected by using the **error** namespace in the destination. The next example bounces email addressed to **spam@tccorp.com** with the message **5.7.0:550 Invalid address**:

```
spam@tccorp.com                        error:5.7.0:550 Invalid address
```