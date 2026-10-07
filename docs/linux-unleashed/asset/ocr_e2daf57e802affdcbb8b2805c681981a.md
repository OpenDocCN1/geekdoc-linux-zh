# Using FTP

It doesn’t matter whether you are on a Linux system, a UNIX machine, a Windows PC, or a Macintosh. When you are ready to use FTP to transfer files, you start a client FTP software package, specify the name of the remote system you want to connect to, then let the two machines establish an FTP session. After you are connected, you can start transferring files.

Character-based FTP is usually started with the name or IP address of the target machine. GUI-based FTP clients usually display a window first, from which you can select a Connect option or the name or IP address of the remote system from a list. If you use a machine name, such as “darkstar” or “superduck,” the name must be resolvable into an IP address by your system for FTP to connect.

When FTP successfully connects to the remote machine, you normally must be able to log in with a valid user login and password. Some systems allow an anonymous or guest login. On large networks where a system such as Yellow Pages (YP) or Network Information Services (NIS) is used, logins are usually permitted across the network onto most machines. If YP or NIS is not employed on your LAN, you must be in the valid user file of the remote machine to obtain FTP access (except for anonymous FTP, of course). You can log into the remote with a different user ID from your local machine’s login (if there is one). To transfer files from one system to another, you must have proper permissions on both systems.

Here’s a very important point: after logging in using FTP, you are not actually on the remote machine. You are still logically on your client machine, and all instructions for file transfers and directory movement are with respect to your local machine and not the remote one. This is the opposite of Telnet, a difference that causes considerable confusion among newcomers to FTP and Telnet.

**WARNING**

Remember that all references to files and directories are relative to the machine that initiated the FTP session. If you are not careful, you can accidentally overwrite existing files.