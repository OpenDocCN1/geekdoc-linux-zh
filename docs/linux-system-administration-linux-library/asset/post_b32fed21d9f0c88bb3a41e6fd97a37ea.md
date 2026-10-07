
inetd. This program's greatest advantage is that it combines many of the features of TCP Wrappers in the super server proper. It's particularly useful on systems that have multiple network cards, because it can block access to particular servers based on the network card.

The xinetd configuration file is /etc/xinetd.conf. Its format is different from that of inetd.conf, but contains much of the same information. Rather than placing information on a single line, xinetd.conf creates multiple-line entries. Listing 15.3 shows the xinetd.conf equivalent of the sample inetd.conf entry shown earlier. This also shows the use of the interface option, which tells xinetd to listen only on the interface associated with the specified IP address. In this example, if the computer has two network interfaces, only one will respond to incoming FTP traffic.

# Listing 15.3 A Sample xinetd.conf Service Entry

```
service ftp
{
    socket_type  = stream
    protocol     = tcp
    wait        = no
    user        = root
    server      = /usr/sbin/in.ftpd
    server_args = -1 -a
    interface   = 192.168.203.7
}
```

Most of the entries in the xinetd.conf service definition correspond to entries in the similar inetd.conf service definition. One exception is the interface entry, which has no inetd.conf service definition. Another difference is that there's no call to tcp in the xinetd.conf definition. This is because xinetd incorporates functionality similar to that of TCP Wrappers. In particular, you can use only_from to specify a list of IP addresses, networks, or computer names that are allowed to use a service; or you can use no_access to "blacklist" computers or networks, blocking them from using a service. You can also block access based on time of day, limit the total number of connections to a service, and so on. These options and many more are detailed in the xinetd.conf page.

The default Red Hat 7.0 xinetd.conf file is quite short. Instead of listing entries for all services in a single file, Red Hat 7.0 uses a xinetd.conf file that sets only global default options.

# In Sum

Files for specific servers appear in the /etc/xinetd.d directory. This configuration makes it easy for server packages to set themselves to run when they are installed. If you're using xinetd on another distribution, you may prefer to maintain a monolithic xinetd.conf file with entries for all your servers. Both approaches are perfectly valid.

After making changes to your xinetd configuration, you must restart the server. You do this much as you restart inetd, as described earlier.

# General Super Server Considerations

Because a super server doesn't keep the real servers loaded at all times, you do not normally have to restart the super server if you update the underlying server. You can upgrade the Telnet server, for instance, and the super server will immediately begin using the new version. The exception to this rule is if the updated server needs to be called in a new way—if its name or location has changed, for instance.

The drawback of using a super server is that it necessarily takes some time to launch its “child” servers. The result is that the server computer won't respond immediately to your request; it may take anywhere from a fraction of a second to seconds for the system to respond to a request. This can be a major drawback for some servers, such as Web servers. You have to judge yourself whether the delay is worth the improvement in memory use and (perhaps) security of using a super server.

Some servers don't work well, if at all, from a super server. Most installations don't run Samba or sendmail through inetd or xinetd, for instance; although it's possible to run these servers through a super server, the performance penalty is too great. You should therefore not think that you shut down all unnecessary servers unless you've cleared superfluous servers from /etc/inetd.conf, /etc/xinetd.conf, or /etc/xinetd.d. You may need to clean more from the /etc/init.d directory tree or other system setup files.

# In Sum

TCP/IP networking is the most popular type of networking today. It's the protocol that's used on the Internet, and many local networking tasks use TCP/IP as well. Configuring Linux for TCP/IP networking involves using a handful of tools to activate a network interface, tell Linux how to route packets, and so on. Most distributions allow you to configure these options when you install the OS, or you can do it after-the-fact through either a GUI configuration utility or by editing configuration files in a text editor.

![](img/4fb617eb648f87def380ef5d92052d01_564_0.png)

PART 5

File sharing is one of the most popular networking tasks on small networks. This task builds on basic TCP/IP networking features, allowing you to store files on a single computer for use by many systems. This can be a great boon in many work environments, boosting productivity by allowing individuals to work at any computer and to exchange files among themselves easily.

Linux supports a wide variety of TCP/IP-based Internet servers, which can provide private and public services to remote systems. Many of these servers are the topics of entire books. Chapters 16 and 17 introduce two of these services, the X Window System and mail servers.

# 16

## The X Window System

Graphical user interfaces (GUIs) are practical necessities for many computer users today. Although it's possible to accomplish a lot with text-mode tools, many users are more comfortable in a GUI environment than with text-mode programs. GUIs are also extremely useful for certain classes of programs, such as graphics editors. Some OSs, such as macOS, integrate their GUIs extremely tightly into the OS as a whole. Linux uses a looser arrangement, however. In Linux, the GUI is entirely separate from the core of the OS. In fact, several different GUIs are available for Linux, but the most common by far is known as the X Window System, or X for short.

Most modern Linux distributions, including Red Hat, make every effort to configure X properly at installation, and to set up defaults that make for an appealing and easy-to-use GUI environment. Such configurations may lead a new Linux user to believe that Linux is more like Windows or macOS than it is. In fact, X is very different from these operating systems in many ways, leading to distinct advantages and disadvantages to X as compared to GUIs in other OSs.

This chapter begins with a look at basic X concepts, such as X as a network protocol. This chapter then proceeds to an overview of X configuration—although, with any luck, this will be handled automatically at system installation time. Then, a discussion is provided of each of three important components of a working X environment: the window manager, widget sets, and the desktop environment. This chapter concludes with a look at some of the issues involved in running X-based applications on a Linux system.

## X Concepts

You're probably already familiar with GUI environments, be it from using Windows, macOS, or some other OS; or from using X on Linux or Unix as a user (as opposed to a system administrator). Much of your knowledge from these experiences can be useful in using and administering X. You should be aware of several unique aspects of X, however. Many of these characteristics make X much more flexible than many other GUIs, but some can be creating or confusion on the part of new users.

## X as a Network Protocol

Compared to other GUI environments, X's most unusual characteristic is that it's a very network-oriented tool. The basic idea behind X is this: when an X-based program is launched on a Linux computer, the program attempts to connect to an X server. The X server provides a screen on which the program can display its output, and a keyboard and mouse to provide for input.

When you set up a Linux computer as a workstation, it defaults to using a local X server for these functions. This X server uses the computer's standard keyboard, mouse, and monitor. Therefore, no actual network accesses are involved. A Linux program can easily direct its requests to an X server running on another computer, however. When this happens, the result is that you can use one computer (on which an X server is running) to run software that's located on another computer (the client). Typically, you use a remote login client (such as Telnet; see Chapter 15) and an X server on the local system, with a login server and X client (the program) on a remote system. After logging in to the remote system, you issue appropriate commands to make its X programs use your local display, and launch an X server locally. The remote system need not even have a display or X server. This arrangement is illustrated in Figure 16.1.

Figure 16.1 The X server runs on the computer at which a user sits; the X client may be located miles away from the user.

![](img/4fb617eb648f87def380ef5d92052d01_567_0.png)
