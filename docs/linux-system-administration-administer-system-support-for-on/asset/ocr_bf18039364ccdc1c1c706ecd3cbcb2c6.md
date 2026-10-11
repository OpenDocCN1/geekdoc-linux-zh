![](bbox=[0.07, 0.08, 0.7, 0.26])

Figure 11-14: Verifying callback information

The next question is authentication. If your ISP uses authentication, they probably use PAP. Some use CHAP, which encrypts the password you send them. PAP authenticates your password connection through cleartext, meaning your password is not encrypted. CHAP does the same thing that PAP does; additionally, it encrypts your password. (See Figure 11-15.)
You can run PPP as follows:

```
stripea:~# ppp-go
```

You don't have to stay in the root window to run since PPP runs from a daemon called pppd. The PPP daemon now controls all your network connections through the ISP and allows you to have Internet access. This is transparent to you, as you are using the ISP's resources (such as their nameserver and routers) to access the Internet. Just go to another window, run Netscape, telnet or ftp to other sites, and so on.

![](bbox=[0.07, 0.63, 0.7, 0.85])

Figure 11-15: PPP authentication