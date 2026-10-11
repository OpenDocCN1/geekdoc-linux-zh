
When you type the command `ping` `server1`, the Sun server will look into the ARP table for the host name `server1` and the IP address that it represents. The `ping` command uses the actual IP address that relates to `server1`.

The following list includes some other utilities you will find useful as diagnostic commands:

- `crash`: A utility that diagnoses core crash dumps.
- `iscda` `script`: A script that is available with a private SunSolve account. The Sun Solution Center support engineers will often request that this script be run for analysis. This script gives the output of the `adb` and `crash` utilities in a convenient format that can be used for quick diagnostics.
- `devlinks`: A utility that re-creates in the /dev directory symbolic links from the /devices directory.
- `eeprom`: A command you can use to view the NVRAM variables from within the operating system. You can also change the value of the variables. The effects of the changes will not be seen until the system is rebooted.
- `grpck` and `pwdck`: Two very useful utilities that check the `passwd` and `group` files for problems.
- `ifconfig`: Command that gives the status of the network interface. It will indicate whether the interface is up and running and give the IP address, sub-net mask, and other status information on the network interface.
- `iostat`: Command that gives the performance of various I/O parameters. It works with the CPU, hard drive, and network card.
- `perf meter`: A GUI utility that gives several parameters that are similar to the parameters given by `iostat`. This utility does require X server software on the server to monitor the utility and an X display on the client to view the results.

Many of these utilities are documented in the Solaris man pages or can be found in AnswerBook2.

## System Communication

There are four primary means of communication with a Sun server or workstation:

- A keyboard, mouse, and monitor directly connected to the server
- A terminal server connected to serial port A
- A network connection through a network card
- A PPP or SLIP connection through a modem

A network connection is typically through an Ethernet card. The first step in troubleshooting network problems is to use the command `ping 127.0.0.1` and look for a `<servername> is alive` response. The IP address 127.0.0.1 is a local loopback address used for testing and internal TCP/IP operations. If you cannot ping 127.0.0.1, double-check the `/etc/hosts` file for typing errors.

Ping the address of the local Ethernet card to see if it is up. Then try pinging the default router's IP address. When a Sun server does not know where an IP packet should be sent, it will send the packet to the default router. The default router is the first router the server is capable of contacting. Any further IP resolution is performed by the default router and is of no further concern to the server. If you cannot contact your default router, you will have no further communications to the network through that particular network interface. To test the default router, ping its IP address, as in the following command (where ###.###.###.### is the IP address of the default router):

```
ping ###.###.###.###
```

The default router is defined by the file `/etc/defaultrouter`.

> **TIP**
> Solaris sends only packets that are not destined for computers on its local network to the router. If the Sun workstation believes that the IP address it is trying to reach is part of its local network, then it will attempt to send the packets directly to the system and ignore the router.

If you still can't ping the router, make sure the router itself is up and running. Try pinging the router from another server and see if that server has a ping response from the default router's IP address. The next step would be to double-check the Ethernet cable between the network interface and the default router's Ethernet port. Before trying to go to another system to ping the router, you should attempt to ping one other system on the same subnet. You should then check the cable from the workstation to the network.

If you cannot reach this Ethernet IP address, double-check three files: `/etc/hosts`, `/etc/netmask`, and `/etc/defaultrouter`. These three files define the IP address, the subnet mask, and the default router.

There is another command that is useful for diagnosing the Ethernet card itself, the `ifconfig` command. There are actually two different versions of `ifconfig`: `/usr/sbin/ifconfig` and `/sbin/ifconfig`. The `/sbin/ifconfig` is used by the Solaris operating system itself to configure the network interfaces during the system boot-up. The `/usr/sbin/ifconfig` is affected by a file named `/etc/nsswitch.conf`. The file `/etc/nsswitch.conf` determines if a Sun server will receive its configuration information locally or from a remote source like an NIS server or a DNS server. So, the `/sbin/ifconfig` command works only with local files, whereas the `/usr/sbin/ifconfig` command will work with network information sources like NIS or DNS if that option is specified in `/etc/nsswitch.conf`. The command `ifconfig -a` shows the output from all the network cards.

> **NOTE**
> The output of `ifconfig` and its use are covered in Chapter 9, “Network Services.”

## Applications and Scripts

The Solaris operating system runs a series of startup scripts from the directories `/etc/rc2.d` and `/etc/rc3.d`. These are Bourne shell scripts that set up environmental variables, initialize hardware, and configure the operating system. They can be modified to customize the server for a particular environment. Unfortunately, sometimes these run control scripts can have typos or other problems that prevent their successful execution. During the startup process, it is possible to press Ctrl+C to skip the execution of a faulty script. This could cause some problems, though, because some variables won’t be set properly or some executable files won’t be run. You can manually run these scripts by hand to check their operations. For example, you can run the script `/etc/rc3.d/S15NFS.server`. To disable a particular script (to prevent it from running), change the first letter of the script from an uppercase S or K to a different letter or number.

Another check for run control scripts is to copy the lines out of the script and run them on the command line. You could, for example, run the line `/opt/SUNWvm/vm` on the command line to see if the process is running. Basically you are executing particular statements manually and seeing the results of these actions.

Most of the Sun Solaris scripts have been thoroughly tested by Sun. Check the file’s last modification time (using the `ls`, or `list`, command) to see if anyone has modified the file since the original installation date. If the file still has the same initial creation date, open the file with the `vi` command and make sure it has valid text lines. The script should be executable by root only, so double-check this permission.

All the scripts should have roughly the same date and time, and they should correspond to the initial installation date. If a run control script is very badly damaged or corrupted for some reason, you might be able to copy the script from the install CD-ROM or from another well-functioning Sun computer of the same system type.

During the startup process, a series of text messages is displayed. The **dmseg** command displays the initial startup messages. You can also check these messages by viewing the text file `/var/adm/messages`.

If you type the name of an application and it does not run, it may be that the application is not in the user's path. If a command or shell script is not in a user's path, the command will not be recognized (which is a common problem). To run an application outside the path, use this command:

`./<application>`

This will run the command from the current working directory. To view the path variable, type the following command:

`echo $PATH`

Sometimes there are multiple copies of a command. For example, as mentioned earlier, there are two versions of **ifconfig**. There is an `/sbin/ifconfig` and a `/usr/sbin/ifconfig`. To know which version of a command you are running, type this command (this shows the path to the command being selected):

`which command`

You could also have a problem with file and directory permissions. The user needs to have executable permissions to a command. The executable permission can be a user, group, or other executable permission. The command `ls -l` will show all the permissions on the command.

The command `id <username>` will show the user ID and group ID of a user. Once you know who the file belongs to, the final step is to make sure the file is not corrupt. The command `file` will run a series of tests on a file. Check the file's size, and if it is unusually small (say, 0MB) or unusually large (like 3MB), the file could be corrupt.

If none of these commands work, try reloading the software package or just the executable file itself. The only other option is to check the operating system version and patch level. Often developers will compile an executable on a specific Sun version and patch level. Later patches and operating systems may not be compatible with the compiled executable. You can either recompile the code yourself (if you have the source code) or change the patch level to match the executable's patch level. The command `showrev -p` shows all the patches on the system.

## Following Program Execution

If an executable will run but something goes wrong during its execution, you can try the **truss** command to follow the program's execution. The **truss** command will
