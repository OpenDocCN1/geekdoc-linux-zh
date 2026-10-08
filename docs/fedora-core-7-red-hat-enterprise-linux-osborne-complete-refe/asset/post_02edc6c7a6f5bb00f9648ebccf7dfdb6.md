
## NcFTP

The NcFTP program has a screen-based interface that can be run from any shell command line. It does not use a desktop interface. To start up NcFTP, you enter the **ncftp** command on the command line. If you are working in a window manager, such as KDE, GNOME, or Xfce, open a shell terminal window and enter the command at its prompt. The main NcFTP screen consists of an input line at the bottom of the screen with a status line above it. The remainder of the screen is used to display commands and responses from remote systems. For example, when you download files, a message specifying the files to be downloaded is displayed in the status line. NcFTP lets you set preferences for different features, such as anonymous login, progress meters, or a download directory. Enter the **pref** command to open the preferences screen. From there, you can select and modify the listed preferences.

To connect to an FTP site, you enter the **open** command on the input line, followed by the site’s address. The address can be either an IP address or a domain name, such as **ftp.gnome.org**. If you don’t supply an address, a list of your bookmarked sites is displayed, and you can choose one from there. By default, NcFTP attempts an anonymous login, using the term “anonymous” as your username and your e-mail address as the password. When you successfully connect, the status bar displays the remote site’s name on the left and the remote directory name.

If you want to log in to a specific account on a remote site, have yourself prompted for the username and password by using the *-u* option with the **open** command. The **open** command remembers the last kind of login you performed for a specific site and repeats it. If you want to change back to an anonymous login from a user login, you use the *-a* option with the **open** command.

Once connected, you enter commands on the input line to perform FTP operations such as displaying file lists, changing directories, or downloading files. With the **ls** command, you can list the contents of the current remote directory. Use the **cd** command to change to another remote directory. The **dir** command displays a detailed listing of files. With the **page** command, you view the contents of a remote file, a screen at a time. To download files, you use the **get** command, and to upload files, you use the **put** command. During a download, a progress meter above the status bar displays how much of the file has been downloaded so far. The **get** command has several features described in more detail in the following section. When you finish, you can disconnect from the site with the **close** command. You can then use **open** to connect to another site, or quit the NcFTP program with the **quit** command. The **help** command lists all NcFTP commands. You can use the **help** command followed by the name of a command to display specific information on it.

The NcFTP **get** command differs significantly from the original FTP client’s **get** command. Whereas the original FTP client uses two commands, **get** and **mget**, to perform download operations, NcFTP uses only the **get** command. However, the NcFTP **get** command combines the capabilities of both **mget** and **get** into the **get** command, as well as adding several new features. By default, the NcFTP **get** command performs wildcard matching for filenames. If you enter only part of a filename, the **get** command tries to download all files beginning with that name. You can turn off wildcard matching with the *-G* option, in which case you must enter the full names of the files you want.

## Chapter 15
Network Tools

You can use a variety of network tools to perform tasks such as obtaining information about other systems on your network, accessing other systems, and communicating directly with other users. Network information can be obtained using utilities such as ping, finger, traceroute, and host. Talk, ICQ, and IRC clients enable you to communicate directly with other users on your network. Telnet performs a remote login to an account you may have on another system connected on your network. Some tools have a corresponding K Desktop or GNOME version. In addition, your network may make use of network remote access commands. These are useful for smaller networks and enable you to access remote systems directly to copy files or execute commands.

### Network Information: ping, finger, traceroute, and host

You can use the ping, finger, traceroute, and host commands to find out status information about systems and users on your network. The ping command is used to check if a remote system is up and running. You use finger to find out information about other users on your network, seeing if they are logged in or if they have received mail; host displays address information about a system on your network, giving you a system's IP and domain name addresses; and traceroute can be used to track the sequence of computer networks and systems your message passed through on its way to you. Table 15-1 lists various network information tools.

| Network Information Tools | Description |
|---|---|
| ping | Detects whether a system is connected to the network. |
| finger | Obtains information about users on the network. |
| who | Checks what users are currently online. |
| whois | Obtains domain information. |
| host | Obtains network address information about a remote host. |
| traceroute | Tracks the sequence of computer networks and hosts your message passes through. |
| ethereal | Protocol analyzer to examine network traffic. |
| gnome-nettool | GNOME interface for various network tools including ping, finger, and traceroute. |
| mtr and xmtr | My traceroute combines both ping and traceroute operations (Traceroute on System Tools menu). |

**TABLE 15-1** Network Tools

### GNOME Network Tools: gnome-nettool

For the GNOME desktop, the gnome-nettool utility provides a GNOME interface for entering the ping and traceroute commands, as well as Finger, Whois, and Lookup for querying users and hosts on the network. Applications | System Tools | Network Tools. Whois will provide domain name information about a particular domain, and Lookup will provide both domain name and IP addresses. You can access gnome-nettool with the Network Tools entry in the System Tools menu. It also includes network status tools such as netstat and portscan, which are described in more detail in Chapter 35. The first panel, Devices, describes your connected network devices, including configuration and transmission information about each device, such as the hardware address and bytes transmitted. Both IPv4 and IPv6 host IP addresses will be listed (see Chapter 35 for more information on addresses).

### ping

The **ping** command detects whether a system is up and running. **ping** takes as its argument the name of the system you want to check. If the system you want to check is down, **ping** issues a timeout message indicating a connection could not be made. The next example checks to see if www.redhat.com is up and connected to the network:

```bash
# ping www.redhat.com
PING www.redhat.com (209.132.177.50) 56(84) bytes of data.
64 bytes from www.redhat.com (209.132.177.50): icmp_seq=1 ttl=118 time=36.7 ms
64 bytes from www.redhat.com (209.132.177.50): icmp_seq=2 ttl=118 time=36.9 ms
64 bytes from www.redhat.com (209.132.177.50): icmp_seq=3 ttl=118 time=37.4 ms

--- www.redhat.com ping statistics ---
4 packets transmitted, 3 received, 25% packet loss, time 3000ms
rtt min/avg/max/mdev = 36.752/37.046/37.476/0.348 ms
```

You can also use **ping** with an IP address instead of a domain name. With an IP address, **ping** can try to detect the remote system directly without having to go through a domain name server to translate the domain name to an IP address. This can be helpful for situations where your network’s domain name server may be temporarily down and you want to check if a particular remote host on your network is connected. In the next example, the user checks the Red Hat site using its IP address:

```bash
# ping 209.132.177.50
PING 209.132.177.50 (209.132.177.50) 56(84) bytes of data.
64 bytes from 209.132.177.50: icmp_seq=1 ttl=118 time=37.4 ms
64 bytes from 209.132.177.50: icmp_seq=2 ttl=118 time=37.0 ms
64 bytes from 209.132.177.50: icmp_seq=3 ttl=118 time=36.3 ms
```
