To access a remote font server, revise the directive to have the form:

```
Font Path `tcp/server:7100`
```

where server is the host name or IP address of the host running the font server. You must also modify the /etc/rc.d/init.d/xfs file. Change the line

```
daemon xfs -droppriv -daemon -port -1
```

to read

```
daemon xfs -droppriv -daemon -port 7100
```

![](bbox=[0.138, 0.353, 0.203, 0.401])

By default, an X font server listens on port 7100. However, you can assign another port, if you prefer. To do so, modify the font server configuration file, /etc/X11/fs/config, and the font server SysVinit file, /etc/rc.d/init.d/xfs. See the xfs page for details.

Now, configure a remote font server by completing Exercise 28.5.

> EXERCISE 28.5
 Configuring a Client to Use a Remote X Font Server

To test your understanding of xfs, configure a client host to use the X font server running on a remote server.

You can consult this book and other documentation to help you complete this exercise. But, before taking the RHCE exam, be sure you can configure a remote X font server without help.

# Summary

In this chapter, you learned about configuring and using remote X servers and clients. The most important topics covered are:

+   X Security X implements a simple host-based security system. You can configure which hosts are allowed to access an X server by using the host command.

+   Remote X Clients The DISPLAY environment variable specifies the X server, which can reside on a remote host.