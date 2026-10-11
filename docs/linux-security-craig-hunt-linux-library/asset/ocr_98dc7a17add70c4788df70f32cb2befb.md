tcp    0    0    *:ssh    *:*    LISTEN
tcp    0    0    *:socks    *:*    LISTEN
raw    0    0    *:icmp    *:*    7
raw    0    0    *:tcp    *:*    7

The netstat --inet -a command in Listing 4.11 shows the connections that are currently active (ESTABLISHED) or in the process of being torn down (CLOSE_WAIT), as well as those services that are currently awaiting new connections (LISTEN). You need to focus on this latter category and look for those services that appear after the host name (and the period) under the Local Address column. In fact, I often create a script that e-mails me the output of the following netstat command periodically:

```
[ramon]$ netstat --inet -a | grep LISTEN
tcp    0    0    *:telnet    *:*    LISTEN
tcp    0    0    *:ftp    *:*    LISTEN
tcp    0    0    *:www    *:*    LISTEN
tcp    0    0    *:smtp    *:*    LISTEN
tcp    0    0    *:ssh    *:*    LISTEN
tcp    0    0    *:socks    *:*    LISTEN
```

The previous output from the netstat command is the most accurate picture of what your Linux server looks like to a potential intruder. There are a total of six services active, and there are service names for all of them. (I had to add the service name socks to /etc/services by hand; otherwise I would simply see port 1080.)

The challenge is to make sure that the services listed by this command are those that your security policy currently allows, and to make sure that you have TCP Wrappers configurations for all these services.

Also, make sure to update the daemons that serve these ports with the latest security fixes and monitor their log files several times daily. If you follow these basic guidelines, you’ll have a very close grip on the network configuration of your server.