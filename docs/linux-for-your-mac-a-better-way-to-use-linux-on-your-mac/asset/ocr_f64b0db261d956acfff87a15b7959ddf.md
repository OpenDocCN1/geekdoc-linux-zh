If you have a LAN connected to the Internet, chances are more than good that you or your system administrator has a `firewall` in place. A firewall can be built using software or hardware. But the basic idea is to protect your system from intruders whose ultimate aim is to gain access as the root operator. Once an intruder gains access as root, all is lost, and you are at someone else’s mercy.

# ## Basic Firewalling

If you don’t want to offer a tempting target, turn off all unwanted network services. Review your system’s `/etc/inetd.conf` file to see what services are turned on. If you see a service, such as Internet Relay Chat, and you don’t use it, turn it off! Make sure that you have system logging enabled (through the use of the `syslogd` daemon), and take the time to examine your logs once in a while. Nearly all Linux distributions log system and kernel activity to a file named `messages` under the `/var/log` directory. You can read this file (as root) by using a pager command, such as `less` like this:

```
# less /var/log/messages
```

Another thing you can do is turn to various software packages that can help provide a measure of security by filtering access into and out of your system.

First, don’t use a root password that is easily cracked. This includes using any word from your system’s dictionary, `/usr/dict/words`. Change your root password often, and review your system’s users often. Some Linux distributions also provide for password aging, and you can use the `expiry` command to set up rules for password aging.

If you have an Internet connection, physically separate your LAN from the Internet and place a hardware router, DSL router, or share partner between your LAN and the Internet. This spare computer will then have two Ethernet interfaces through which traffic is routed. If you’re ultra security conscious, install the OpenSSH (*Open Secure Shell Server*) and related `ssh` utilities.

Next, use `ipchains` (for 2.2.X kernels) to set up a ruleset for packet filtering. For advice on how to best set up a system, see Rusty Russel’s Linux IPCHAINS-HOWTO. Most Linux users create a shell script containing the necessary commands and rules. Once a ruleset has been devised for your system (to filter various service packets), use the `ipchains-save` command to save your settings.

If you use SUSE Linux, you can use the `yast` command to also perform some basic settings. Start `yast`, select System Administration, then Security Settings. Next, press Enter on Configuration of `/etc/login.defs`. You’ll see a dialog box as shown in Figure 15.12.