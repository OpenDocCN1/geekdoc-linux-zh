
## Browse Options

This option controls whether the printer share can be seen in the Network Neighborhood.

## Miscellaneous Options

The few options that are available here are the same as those that are found in the Shares section under Miscellaneous Options.

## Restricting Access to Services

The Samba server configuration is extremely flexible. It can make use of UNIX NIS groups for access control, giving certain users read-only access, others read-write access, some users admin access, and still others no access. It can also force all users to be treated as members of the guest account (which is, by default, the UNIX user nobody) or as another special user. It can force users to belong to a certain group. All these options and more are part of the Shares page, in the Security Options section under Advanced View. Specifically, these options are Valid and Invalid Users, Admin Users, Read List, Write List (which is both Read and Write), Force User, and Force Group.

By making use of these advanced options, very tight control can be maintained over users’ connections to any given share. An option is also on the Global page to set a root directory to something other than the default of /.

> **Caution**
> 
> If you set the root directory, make sure that everything that is required to run the Samba server, plus binaries and all the libraries that are used by users, is copied below this new root directory. This functions the same as the FTP chroot command.

## Variables Available to Samba

If you’ve followed along in swat and looked at any of the default entries on the Advanced View pages, you’ve seen variables in the form %X, where X is one of many upper- or lower-case letters. These variables can be used to extend the flexibility of Samba. Following is a list of the variables and a short explanation of each:

- `%S`—The name of the current service, if any.
- `%P`—The root directory of the current service, if any.
- `%u`—Username of the current service, if any.
- `%g`—Primary group name of `%u`.
- `%U`—Session username (the username that the client requested, not necessarily the same as the one received).
- `%G`—Primary group name of `%U`.
- `%H`—The home directory of the user (`%u`).
- `%v`—The Samba version.
- `%h`—The Internet hostname (DNS) on which Samba is running.
- `%m`—The NetBIOS name of the client machine.
- `%l`—The NetBIOS name of the server. This enables you to change your configuration based on what the client calls you. Your server can have a dual personality.
- `%M`—The Internet name (DNS) of the client machine.
- `%N`—The name of your NIS home directory server. This is obtained from your NIS auto.map entry. (Without NIS, this is the same as `%L`).
- `%p`—The path of the service’s home directory, obtained from your NIS auto.map entry. The NIS auto.map entry is split up as `%N:%p`.
- `%R`—The selected protocol level after protocol negotiation. It can be CORE, COREPLUS, LANMAN1, LANMAN2, or NT1.
- `%d`—The process ID of the current server process.
- `%a`—The architecture of the remote machine. Only some are recognized, and those might not be 100% reliable. It currently recognizes Samba, WfWg, WinNT and Win95. Anything else is UNKNOWN.
- `%I`—The IP address of the client machine.
- `%T`—The current date and time.

## TROUBLESHOOTING

> *SWAT doesn’t appear to be working for me. When I type http://localhost:901, I get a connection refused error.*

Ensure you have an entry in `/etc/services` like this:

```
swat             901/tcp             # Samba Web Administration Tool
```

Also ensure you have an entry in `/etc/inetd.conf` like this:

```
swat    stream  tcp     nowait.400 root    /usr/sbin/tcpd swat
```

Stop and start inetd:

```
/etc/rc.d/init.d/inet stop && /etc/rc.d/init.d/inet start
```

Grep netstat’s output for an open port 901:

```
netstat -an | grep 901
tcp        0      0.0.0.0:901        0.0.0.0:*        LISTEN
```

If the results of the first line above yield the second line, you should get a login prompt from swat.

> *I get a login prompt, but I am denied access.*

Make sure you are logging in as root exactly as you would if you were logging in to the system.

Ensure you have an `/etc/pam.d/swat` file. For more information see Chapter 15, “Understanding PAM.”

Also make sure that you’re not denying yourself entry via the `/etc/hosts.allow/hosts.deny` files. You can check it by entering this:

```
tcpdmatch swat localhost
```

This assumes you used as an address to access swat:

```
http://localhost:901/
```

If you used something different, substitute whatever you used for localhost in the tcpdmatch statement above. You should get the following as the last line:

```
access: granted
```

> *I can’t seem to connect to any of the Windows hosts. Every time I try to connect, I am asked for a password, and no matter what I put in, I’m denied access.*

One problem you can encounter is that your usernames and passwords are different between your Windows account and your Linux account. They must be the same. If they are, ensure that in the Global Options sections you have `encrypt passwords = yes`.

> *I’m having trouble printing. Seems no matter what I try, all I get is garbage—pages of it.*

Printing is one of those areas that are not well-understood by many, so let’s try to make it simple:

- **Linux/UNIX**—Clients send what they want printed as text (formatted or not) or post-script. Clients know nothing about the printer. The print server knows all about the printer and how to handle either text or postscript, and performs all the formatting. In the Linux/UNIX world, then, if an administrator changes a printer and makes a quick change to the filter and any of the thousands of clients know no different, jobs flow as usual because they always send postscript (or ASCII text).
- **Windows**—Servers know nothing about the printers, they just queue jobs. Clients are expected to micro-manage print jobs and know all about all the printers on the network, so they must send print jobs specifically formatted for the printer to which they want to print. In the Windows world, every client, no matter where they are in the world, must know every detail about the printer they are sending to because the client must format the output. If an administrator changes a printer out, all clients must know about it and change their setup.

You must choose which way to do things. Obviously, if the printer is connected to the Windows system, the Linux system must send the print job formatted for that specific printer (see the information on “bounce queues” (bq) in Chapter 31, “Printing”).

If the printer is connected to the Linux system, you can either have all Windows systems send postscript format or you can set up a raw print queue on the Linux system and send preformatted output to the raw (no print filter) queue. But you can’t send preformatted output to a print filter or you’ll receive garbage from the printer.

> *I created a HOMES share, but my users can’t exchange files. How can I fix that?*

You must set up another share for them pointed at a directory (/tmp works well) where they can share files. Any user connecting to the Linux box HOMES share is relegated to their own directory, and only their own directory.

> *I connected to my Linux (Windows) system from Windows (Linux). I’m trying to run programs from one onto the other. I can see the program, and it’s executable, so why can’t I run it?*

You cannot run Linux binaries on Windows and vice-versa. Each accesses the system through hooks, but the hooks are different on each system, so the binaries won’t run on the other system.

## CHAPTER 30: Setting Up a Network

In this chapter

- About Networking 564
- Hardware 564
- Assumptions 567
- The Individual Systems 568
- The Server 571
- Miscellany 572
- Troubleshooting 574
