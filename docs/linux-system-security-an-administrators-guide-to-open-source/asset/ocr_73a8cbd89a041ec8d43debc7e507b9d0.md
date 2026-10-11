**Table 10.10 Extended Internet Services Daemon Attributes (Continued)**

| Attribute | Description and Allowed Value |
| :--- | :--- |
| `log_on_failure` | Specifies the information to be logged on failure. A message indicating the nature of the error is always logged. Possible values are<br>ATTEMPT: Records a failed attempt. All other values imply this one.<br>HOST: Client host IP address.<br>USERID: Captures UID of the client user through an RFC41413 call. Only available for multithreaded, streams services.<br>RECORD: Records additional client information such as local user, remote user, and terminal type.<br>By default, nothing is logged. This attribute supports any operators. |
| `disabled` | Available for use only with the special `defaults` entry (see *The defaults Entry* on page 237). Accepts a space-separated list of services that are unavailable. It has the same effect as commenting out the service entry in the `/etc/xinetd.conf` file. |

Before we examine Table 10.10, let’s consider a simple example. In Example 10-39, we see a partial /etc/xinetd.conf file. Notice that, in spite of the formatting differences, the information contained in these records is identical to what is found in /etc/inetd.conf (see Example 10-2 on page 195). The reason that these two entries look so similar is because they were generated from /etc/inetd.conf with the itox utility, which simply converts /etc/inetd.conf entries to the proper syntax for xinetd. In this case, the attributes (everything inside the braces and to the left of the = symbol) are very straightforward in their meaning as are the associated values (everything inside the braces and to the right of the = symbol).

# **Example 10-39 Partial /etc/xinetd.conf File**

```
service ftp
{
        socket_type       = stream
        protocol          = tcp
        wait              = no
        user              = root
        server            = /usr/sbin/in.ftpd
        server_args       = -l -a
}

service telnet
{
        socket_type       = stream
        protocol          = tcp
        wait              = no
        user              = root
        server            = /usr/sbin/in.telnetd
}
```

The easiest way initially to create the /etc/xinetd.conf file is with the itox utility. The syntax for its use is simply (this example assumes that the current working directory is the xinetd build directory)