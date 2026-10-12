```
> .D(client_addr)127.0.0.1
> Basic_check_relay <>

rewrite: ruleset 190     input: < >

rewrite: ruleset 190 returns: OKSOFAR
```

This tells you that the address test using 127.0.0.1 (loopback address) is not blocked in RBL, because the rewrite result was OKSOFAR.

+   3. Now, duplicate the preceding test using 127.0.0.2 (the RBL-supplied test IP, which is blocked in RBL). You should see output similar to the following:

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)

Enter <ruleset> <address>
> .D(client_addr)127.0.0.2
> Basic_check_relay <>

rewrite: ruleset 190     input: < >

rewrite: ruleset 190 returns: $$ error $$ 5 . 7 . 1
$ : "Mail from " 1 2 7 . 0 . 0 . 2 * * refused by blackhole site rbl.maps.vix.com. Email from your server is blocked. Contact your local Systems Administrator or ISP."
```

As you can see, this IP is blackholed or blacklisted in RBL, and therefore sendmail will not allow it to relay messages.

You can also perform a real test using an autoresponder that Russell Nelson has put together. According to the autoresponder owner, you must send mail to nelson-rbl-test@crynwr.com from the server whose RBL blocking you want to test. Expect one reply from ns.crnwr.com with the SMTP conversation. If you get another reply from linux.crnwr.com, your RBL setup is not working.

> **Tip**
> If you want to know which mail transactions are rejected because of RBL, simply run `grep "maps.vix.com" /var/log/mail log` to see the rejected requests.