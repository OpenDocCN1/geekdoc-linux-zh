operational with an IP address for the target machine. The dummy interface essentially sets an IP address for your local machine that is valid as far as TCP/IP is concerned, but doesn’t really get used except to fool applications.

Creating a dummy interface is very simple. If your machine has an IP address already assigned for it in the /etc/hosts file, all you need to do is set up the interface and create a route. The following two commands are required:

```
ifconfig dummy machine_name
route add machine_name
```

Where machine_name is your local machine’s name (such as darkstar). This creates a link to your own IP address. If you do not have an IP address for your machine in the /etc/hosts file, you should add one before you create the dummy interface.

# # Configuration Files

Configuring Linux for TCP/IP is not difficult because only a few configuration files need to have the information about IP addresses and such added to them. You can do this with any editor, as long as it saves the files in ASCII format. It is advisable to make copies of the configuration files before you modify them, just in case you damage the format in some way.

Many of these files are similar in every version of UNIX, including most versions of Linux, except for one or two slight naming variations. If you’ve ever set up a UNIX system (or snooped around one in detail), these files and steps might seem familiar. If you haven’t done anything with Linux or UNIX before, just take it one step at a time and follow the instructions.

# # rc Files

Linux reads the rc (run command) files when the system boots. The init program initiates the reading of these files, and they usually serve to start processes such as mail, printers, cron, and so on. They are also used to initiate TCP/IP connections. Most Linux systems have the rc command files in the directory /etc/rc.d.

The two files of interest to TCP/IP are rc.inet1, which sets the network parameters, and rc.inet2, which starts the daemons used by TCP/IP. On some systems, these two files are combined into one larger file called either rc.inet or rc.net.

To configure the rc.inet files to start up the TCP/IP network, you must first make sure that the files are actually read by the init program. This is handled by the /etc/inittab and /etc/rc.d/rc.M files, where there are one or more lines that control the reading of the rc.inet files.