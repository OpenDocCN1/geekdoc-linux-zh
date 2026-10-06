# Chapter 10 • Securing Your System

accessible ports that would not be accessible from the outside world. On the other hand, a cracker on your local network would likely have access similar to yours, so you shouldn't be complacent because you use a firewall. Nonetheless, firewalls can be important tools for hiding servers without shutting them down.

You can use a stand-alone Linux boot CD-ROM to perform security checks on a network. Tools intended for this purpose, such as BackTrack (http://www.backtrack-linux.org), provide easy access to Nmap and other network security tools, enabling quick checks of network security even if no computer on that network regularly Linux.

# Examining Configuration Files

Linux server packages include configuration files. Thus, you may be able to spot installed but unwanted servers by looking for their configuration files. On most systems, two classes of files are important: controlling startup scripts and controlling your super server.

Startup scripts are described in Chapter 5, so review for details of how they're managed. Generally speaking, you'll look in /etc/rc.d, /etc/init.d/rc?, or or /etc/rc/rc?, where ? is your default runlevel number, SysV startup scripts whose names take the form S#, where # is a number and the name of the server. If you find a script for a server you know don't want to run, you should disable it using your SysV startup script editing tools, as described in Chapter 5. If your distribution uses Upstart or systemd, though, you'll need to look elsewhere for the relevant startup files.

Be aware that many startup scripts start subsystems that aren't directly network-related. Thus, you'll probably see startup scripts that you don't recognize. You shouldn't automatically disable these scripts, because they may be necessary even if you don't recognize the name. If in doubt, leave it in until you can research the matter further.

Try to do a Web search on the name of the startup script (minus the S and sequence number or other components unique to your startup system), in conjunction with "Linux" or "startup script." Chances are, you'll find a helpful reference.

The other major configuration-file you should examine is the super server configuration. Thus, you should check inet or systemd configuration files for unwanted servers. Also, unlike system startup scripts, super servers launch network servers only, not non-network services. Therefore, you should take a more aggressive approach to disabling entries you don't recognize from your super server configuration than you do with system startup scripts.