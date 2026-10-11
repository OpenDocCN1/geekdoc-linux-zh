this Linux host, the inetd daemon will start the tcpd daemon and pass to it the name of the actual daemon to be started (vsftpd) as a server argument. As with xinetd, using TCP wrappers with inetd allows you to control access to the network services running on the host using the `/etc/hosts.allow` and `/etc/hosts.deny` files.
Let's practice configuring super-daemons in the following exercise.

# Exercise 17-3: Configuring xinetd

In this exercise, you'll practice working with xinetd by enabling one of the several services managed by this super-daemon.

![](bbox=[0.15, 0.28, 0.22, 0.38])

> **NOTE** This exercise will require the use of a second Linux system to test your configuration. Both systems need to be connected to, and configured correctly to participate on, the same network segment. In addition, if your Linux distribution uses inetd instead of xinetd, you'll have to adapt the steps using the content presented in this chapter.

You will enable the time service on your Linux host via xinetd. Once done, your Linux host can function as a time provider to time clients. Complete the following:

+   1. Boot your Linux system and log in as a standard user.
+   2. Open a terminal session.
+   3. Switch to your root user account by entering `su` – followed by your root user's password.
+   4. At the shell prompt, use the `cd` command to change to the `/etc/xinetd.d` directory.
+   5. At the shell prompt, enter `vi /time-udp` to open the xinetd configuration file for the time service. You should see configuration settings that are similar to the following:

```
```
service time
{
    type                = INTERNAL UNLISTED
    id                  = time-dgram
    socket_type         = dgram
    protocol            = udp
    user                = root
    wait                = yes
    disable             = no
    port                = 37
    FLAGS               = IPv6 IPv4
}
```
```

![](bbox=[0.15, 0.82, 0.22, 0.94])

> **TIP** There are two different configuration files for the time service.The time file configures time to use TCP while time-udp configures time to use UDP.
> Be sure you are editing the correct version of the file! Notice that the type parameter indicates that the time service is an *internal* service. This means the time service is part of the xinetd daemon itself.There is no external executable file for this daemon.