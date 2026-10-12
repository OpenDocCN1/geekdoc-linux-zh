The preceding class definition allows real users to log on from any machine in the evoknow.com and ad--engine.com domains.

![](bbox=[0.06, 0.24, 0.16, 0.33])

If you are not planning on allowing anonymous or guest accounts on your FTP server, you can remove the “guest” and “anonymous” keywords from the default typelist for the all class.

deny This keyword is used to deny FTP service to hosts that match the IP addresses or domain names specified.

Syntax: deny addrglob message_file

For example, the following instruction tells the FTP server to deny access to anyone trying to access the server from a U.S. university:

```
deny *.edu
```

Here is another example:

```
deny *.com /etc/goaway.msg
```

This configuration denies FTP access to anyone in a .com domain and also displays the /etc/goaway.msg file.

limit This keyword limits the number of simultaneous user logins for the named class.

Syntax: limit class n times message_file

The arguments for limit are as follows:

+   ■ n is the number of users allowed access.
+   ■ times is when the limit should apply. The time can be specified in a 24-hour clock format. For example, 0700–1700 is a range that covers 7 a.m. to 5 p.m. The time format can also include days, as shown in Table 14-1.