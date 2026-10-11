under different credentials (username and password). Disconnect first any existing connection to this network share in order to connect again under a different username and password".

So you close all connections. You try again. You get the same message. You check from the Samba side, using `smbstatus`. Yes, there are more connections. You kill them all. The client still gives you the same error message. You watch the smb.log file on a high debug level and try reconnect. Same error message, but not a single line in the log. You start to wonder if there was a connection attempt at all. You run `ethered` and `tcpdump` while you try to connect. Result: not a single byte goes on the wire. Windows still gives the error message. You close all Explorer windows and start it again. You try to connect — and this times it works! Windows seems to cache connection information somewhere and does not keep it up to date (if you are unlucky, you might need to reboot to get rid of the error message).

The easiest way to forcefully terminate all connections from your client to a server is by executing:

```
```
C:\>  net use * /delete
```
```

This will also disconnect all mapped drives and will allow you create fresh connection as required.

# 20.8.5  Take Care When Assembling Driver Files

You need to be extremely careful when you take notes about the files belonging to a particular driver. Don't confuse the files for driver version "0" (for Windows 9x/Me, going into `[print$]WIN0/0/`, driver version 2 (kernel mode driver for Windows NT, going into `[print$]W32X86/2/`, may be used on Windows 2000/XP also), and driver version "3" (non-kernel mode driver going into `[print$]W32X86/3/`, cannot be used on Windows NT). Quite often these different driver versions contain files that have the same name but actually are very different. If you look at them from the Windows Explorer (they reside in `WIN-DOWS%system32spooldriversW32X86`), you will probably see names in capital letters, while an `enumdrivers` command from Samba would show mixed or lowercase letters, so it is easy to confuse them. If you install them manually using `rpcclient` and subcommands, you may even succeed without an error message. Only later, when you try install on a client, you will encounter error messages like *This server has no appropriate driver for the printer*.

Here is an example. You are invited to look closely at the various files, compare their names and their spelling, and discover the differences in the composition of the version 2 and 3 sets. Note: the version 0 set contained 10 *DependentFiles*, so I left it out for space reasons:

```
```
root# rpcclient -U 'Administrator\secret' -c 'enumdrivers 3' 10.160.50.8

Printer Driver Info 3:
```
```