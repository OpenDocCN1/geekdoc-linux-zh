+   Free chess game:

```
telnet freechess.org 5000
```

The following figure shows a really cool, retro way to play chess... Cool!

![](bbox=[0.163, 0.197, 0.833, 0.606])

OK, enough games for today, now let's get back to learning about other insecure protocols.

# FTP, HTTP, and other unencrypted traffic

Telnet is not the only insecure protocol – other unencrypted protocols such as FTP and HTTP also send unencrypted data that can be easily captured.

As shown in the following figure, the username and password are clearly sent over plaintext when logging in to an FTP server: