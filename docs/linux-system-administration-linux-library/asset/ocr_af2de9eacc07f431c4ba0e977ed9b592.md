# In Sum

options. Files for specific servers appear in the /etc/xinetd.d directory. This configuration makes it easy for server packages to set themselves to run when they are installed. If you're using xinetd on another distribution, you may prefer to maintain a monolithic xinetd.conf file with entries for all your servers. Both approaches are perfectly valid.

After making changes to your xinetd configuration, you must restart the server. You do this much as you restart inetd, as described earlier.

# General Super Server Considerations

Because a super server doesn't keep the real servers loaded at all times, you do not normally to restart the super server if you update the underlying server. You can upgrade the Telnet server, for instance, and the super server will immediately begin using the new version. The exception to this rule is if the updated server needs to be called in a new way—if its name or location has changed, for instance.

The drawback of using a super server is that it necessarily takes some time to launch its “child” servers. The result is that the server computer won't respond immediately to your request; it may take anywhere from a fraction of a second to seconds for the system to respond to a request. This can be a major drawback for some servers, such as Web servers. You have to judge yourself whether the delay is worth the improvement in memory use and (perhaps) security of using a super server.

Some servers don't work well, if at all, from a super server. Most installations don't run Samba or sendmail through inetd or xinetd, for instance; although it's possible to run these servers through a super server, the performance penalty is too great. You should therefore not think that you shut down all unnecessary servers unless you've cleared superfluous servers from /etc/inetd.conf, /etc/xinetd.conf, or /etc/xinetd.d. You may need to clean more from the /etc/init.d directory tree or other system setup files.

# In Sum

TCP/IP networking is the most popular type of networking today. It's the protocol that's used on the Internet, and many local networking tasks use TCP/IP as well. Configuring Linux for TCP/IP networking involves using a handful of tools to activate a network interface, tell Linux how to route packets, and so on. Most distributions allow you to configure these options when you install the OS, or you can do it after-the-fact through either a GUI configuration utility or by editing configuration files in a text editor.

![](bbox=[0.903, 0.716, 0.998, 0.833])

PART 5