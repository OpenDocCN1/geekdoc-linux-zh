# TIP

If you're interested in just the failed attempts, you can easily display all related entries by using grep:

```
Athena:/home/admin # grep -i fail /var/log/xinetd.log
05/1/14@16:28:05: FAIL: echo-stream address from=10.4.4.4
05/1/14@16:29:49: FAIL: echo-stream address from=10.4.4.4
05/1/15@04:43:46: FAIL: echo-stream address from=10.4.4.4
```

# Security Considerations

You should be sure that you need xinetd before you set it up. A client machine that primarily acts as a workstation has no need to run xinetd because the client machine is not meant to provide any services for the network. Similarly, if your SLES server runs a dedicated service, such as DNS, there is also no real need to run xinetd. Whether you use it is basically a question of security. Using xinetd on machines on which you really don't need it may reveal possible entry points for intruders. xinetd-enabled services such as telnet and rlogin can be used to exploit your machine. This doesn't mean that those services are generally insecure, but they may be a first source of information for potential hackers trying to enter your system.

When you are using xinetd, enable only the services that are absolutely required. Typical diagnostic services such as echo and chargen can become targets for DoS attacks because their use diverts CPU resources away from other processes that will cause problems for the connected networks and Internet services dependent on that server.

# Network Time Services

Accurate timing plays an important role in any multithreaded computer operating system. The system kernel schedules processes, and then it processes events based on time. The system time is also used for time-stamping log entries, application transaction records, email messages, security certificate management, and so on. However, unless your server has a built-in atomic clock, to keep proper time, the system clock must regularly be corrected for drifts. You can perform the correction manually or have the system clock updated automatically via some time protocol over the network. SLES 9 includes Network Time Protocol (NTP) software (xntp v4 package) to assist you in obtaining an accurate time from the Internet as well as a way to provide the same correct time to other servers and clients on your internal network. In this section, we