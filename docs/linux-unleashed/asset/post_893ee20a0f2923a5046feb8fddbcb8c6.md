
operational with an IP address for the target machine. The dummy interface essentially sets an IP address for your local machine that is valid as far as TCP/IP is concerned, but doesn’t really get used except to fool applications.

Creating a dummy interface is very simple. If your machine has an IP address already assigned for it in the /etc/hosts file, all you need to do is set up the interface and create a route. The following two commands are required:

```
ifconfig dummy machine_name
route add machine_name
```

Where machine_name is your local machine’s name (such as darkstar). This creates a link to your own IP address. If you do not have an IP address for your machine in the /etc/hosts file, you should add one before you create the dummy interface.

## Configuration Files

Configuring Linux for TCP/IP is not difficult because only a few configuration files need to have the information about IP addresses and such added to them. You can do this with any editor, as long as it saves the files in ASCII format. It is advisable to make copies of the configuration files before you modify them, just in case you damage the format in some way.

Many of these files are similar in every version of UNIX, including most versions of Linux, except for one or two slight naming variations. If you’ve ever set up a UNIX system (or snooped around one in detail), these files and steps might seem familiar. If you haven’t done anything with Linux or UNIX before, just take it one step at a time and follow the instructions.

## rc Files

Linux reads the rc (run command) files when the system boots. The init program initiates the reading of these files, and they usually serve to start processes such as mail, printers, cron, and so on. They are also used to initiate TCP/IP connections. Most Linux systems have the rc command files in the directory /etc/rc.d.

The two files of interest to TCP/IP are rc.inet1, which sets the network parameters, and rc.inet2, which starts the daemons used by TCP/IP. On some systems, these two files are combined into one larger file called either rc.inet or rc.net.

To configure the rc.inet files to start up the TCP/IP network, you must first make sure that the files are actually read by the init program. This is handled by the /etc/inittab and /etc/rc.d/rc.M files, where there are one or more lines that control the reading of the rc.inet files.

Some Linux versions use only the /etc/inittab file to start the TCP/IP daemons. The Slackware version, though, has a line in the /etc/inittab file that tells the init program to read the file /etc/rc.d/rc.M when running multiuser mode. The TCP/IP daemons are not started when the system is in single-user mode.

Whichever file is involved, look for a line that refers to the rc.inet1, rc.inet, or rc.net file. In some cases, this line(s) is commented out (it has a pound sign as the first character) to prevent the system from trying to run TCP/IP when there is no requirement for it. If the line is commented out, remove the comment symbol. The Slackware release of Linux, for example, has an if loop within the rc.M file that has these lines in it:

```
/bin/hostname `cat /etc/HOSTNAME | cut -f1 -d .`
/bin/sh /etc/rc.d/rc.inet1
/bin/sh /etc/rc.d/rc.inet1
```

Make sure that these lines (as well as the if loop that the lines are part of) are not commented out. You want these lines to execute each time the if condition is true. With the Slackware version, the if condition checks for the existence of the file rc.inet1.

If you can't find a reference to the rc.inet files in /etc/inittab, or a pointer to another file that has these files referenced (as with Slackware's /etc/rc.d/rc.M), you will have to add the lines to the /etc/inittab file manually. This can be scary for newcomers to Linux, so make copies of the files so you can always recover. An emergency boot floppy is also always handy to have.

Usually there is a good set of comments within the startup files to help you configure the system. There is a section for TCP/IP Ethernet support that often has a number of lines commented out. It consists of lines like this:

```
#IPADDR="127.0.0.1"
#NETMASK=""
#NETWORK="127.0.0.0"
#BROADCAST=""
#GATEWAY=""
```

Obviously, these correspond to the pieces of information you determined earlier. Therefore, uncomment the lines and type in the information about your machine. If you don't have one of the pieces, such as a gateway address, leave that line commented out. In the rc.inet1 file, please note several references to the programs ifconfig and route. These programs control TCP/IP communications. ifconfig configures network device interfaces, and route configures the routing table.

Near the top of the rc.inet1 file (or whichever file is used in your version of Linux) are a couple of lines that call both ifconfig and route for the loopback driver. The lines probably look like this:

```
/sbin/ifconfig lo 127.0.0.1
/sbin/route add -net 127.0.0.0
```

Neither of these lines should be commented out. They are necessary to set the loopback driver, which must exist on the system in order for TCP/IP to function properly.

There will probably be a number of lines that are commented out below the settings for your machine's IP address with instructions to uncomment one of them. The differences between the lines is whether broadcast and netmask variables are included. To begin, try uncommenting the line that looks like this:

If this causes problems later during system startup, switch the uncommented line to the one that reads

eth0 is the first device for the first Ethernet card on your system, called `eth0`.

Finally, if you have a gateway machine on your network, a section of the `rc.inet1` file lets you enter the IP address of the gateway. Again, these lines should be uncommented. You might want to try to get the system working properly before you set up the gateway because it is easier to debug when the number of potential problems is smaller.

The `rc.inet2` file starts up the daemons used by TCP/IP. In most cases, you won't have to make changes to this file because the most important daemons are usually started anyway. Look for a line that calls the `inetd` program, which is the most important TCP/IP daemon of all. There should be no comments on the line that starts it. It will probably look like this:

```
if [ -f ${NET}/inetd ]
  then
    echo -n " inetd"
    ${NET}/inetd
  else
    echo "no INETD found. INET cancelled."
    exit 1
  fi
```

If you read Chapter 14, "Shell Programming," or you know a little about programming in some other language, this short section might make sense. This routine checks for the existence of the `inetd` file and starts it if it's there. If it's not there, an error message is generated on the display (remember this is during the boot process), and the `rc.inet2` file is exited.

More commented-out daemons are probably listed below inetd, such as named (the name server daemon that converts proper names to IP address), routed (used for routing), and several others. Unless you know that you want one of these daemons active, leave them commented out for now.

One other daemon you might want running is syslogd. It usually is set to execute automatically. This is the system logging daemon, which collects log messages from other applications and stores them in log files. The log file locations, which you can change as you desire, are given in the file /etc/syslog.conf.

That’s enough changes to the rc files for now. After TCP/IP is installed and tested, the rest of the daemons (routed, named, and so on) can be started one at a time to ensure they work. The first task is to get TCP/IP communicating with other machines properly. Then you tweak it!

## /etc/hosts

The /etc/hosts file is a simple list of IP addresses and the hostnames to which they correspond. This is a good location to list all your favorite machines so that you can use the name and have the system look up the IP address. On very small networks, you can add all the machines in the network here and avoid the need to run the named daemon.

Every /etc/hosts file will have an entry for localhost (also called loopback, IP address 127.0.0.1) and probably one for your machine if you named it when you installed the software. If you didn’t supply a name and there is no line other than localhost, you can add it now. Use an editor and set your IP address and machine name. Don’t bother adding too many other machines until you’re sure the network works properly! Here’s a sample /etc/hosts file:

```
127.0.0.1		localhost
147.12.2.42		merlin.tpci merlin
```

You will notice that the format is quite simple: an IP address in one column and the name in another column, separated by tabs. If the machine may have more than one name, supply them all. In the example, which uses random numbers for the IP address, the machine 147.12.2.42 has the name merlin. Because it is also part of a larger network called tpci, the machine can be addressed as merlin.tpci. Both names on the line ensure that the system can resolve either name to the same address.

You can expand the file a little if you want by adding other machines on your local network, or those you will communicate with regularly:

```
127.0.0.1		localhost
147.12.2.42		merlin.tpci merlin
147.12.2.43		wizad.tpci wizard
```
