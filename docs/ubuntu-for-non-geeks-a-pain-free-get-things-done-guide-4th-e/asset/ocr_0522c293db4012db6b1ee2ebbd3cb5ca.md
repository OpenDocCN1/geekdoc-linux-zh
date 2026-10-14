example. Other users on a network can copy files from and (usually) write files to a shared **Documents** folder, whereas they cannot access any other part of the filesystem on that machine.

If the share you are trying to open requires a username and password, you will be asked for those in a new window. Note that, in this case, the username and password you need to enter are those for the machine to which you are trying to connect—not the ones you’re using in Ubuntu (unless the usernames and/or passwords happen to be the same, of course). You can then copy files to and from that share as if it were a folder on your own hard disk.

![](bbox=[0.214, 0.241, 0.899, 0.572])

*Figure 7-7: Viewing the computers on your network*

In some cases, especially when trying to access shares on a Mac running OS X, the double-click method will not work. You will not be able to access any share on a particular machine, even if an icon for that machine appears in the Nautilus window. In such cases, double-click the icon for the machine you are trying to access and then, once open (to an empty window), select **Go › Location**. A text box will appear in the location bar (just like in Figure 7-5) with the location of the machine you are trying to access already listed.

To that location, add a forward slash (`/`) followed by the username used on the target machine. For example, if the target machine is called **cowboycats** and the username is **meatyou**, the location would be `smb://cowboycats/meatyou`. You can also narrow things down to a particular folder on the machine, as long as you know the path to that folder, by adding to the path you’ve already typed; `smb://cowboycats/meatyou/Documents`, for example. If you prefer, you can type `smb://` and your Mac’s IP address, which consists of a set of four numbers