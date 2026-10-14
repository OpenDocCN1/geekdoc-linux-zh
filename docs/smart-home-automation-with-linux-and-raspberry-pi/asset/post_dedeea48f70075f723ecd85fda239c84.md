
This host section can be included within the subnet section shown previously to create exceptions in the pooling rule.

You can determine which leases have been granted by typing the following:

```
more /var/lib/dhcp3/dhcpd.leases
```

Many other options are available in the DHCP server, but these provide enough to get everything working. I'll cover the specific extra cases as appropriate.

## Computer Names

My name is Steven, often shortened to Steve. My computer’s name is 192.168.1.110, which is less easy to remember for nongeeks. Chances are there will be more nongeeks in your house than geeks who will want to refer to each computer by a name such as “Holly’s computer” or “Angela’s laptop.” There are two strains of problem here: getting the computers in the house to have usable names and getting them to know the names of each computer outside the house on the Internet.

Computer names are usually distributed automatically around the local network, so they are not a problem, although it can sometimes take 30 seconds for the information to propagate to all machines. In case of problems, you can force-feed a mapping between IP addresses and computer names by adding a line like this:

```
192.168.1.110    mediapc
```

to the file located at /etc/hosts or C:\WINDOWS\SYSTEM32\DRIVERS\etc\hosts depending on whether you’re working on Linux or Windows, respectively.

Converting Internet domain names into numbers is done through a type of server known as Domain Name System (DNS). This is a simple client/server process whereby a client provides a domain name, such as google.com, and the server returns the globally accessible IPv4 address of the computer. There are many of these servers throughout the world, arranged in a hierarchy. So, if your local DNS server doesn’t know about a particular domain, it will ask its parent DNS server, and so on, all the way up to the master root zone server. All you need to do is configure your home machines to use the first DNS server in this chain, and the searches will happen automatically. If your ISP has provided you with a DNS server address, you can use this directly. Alternatively, if you are using a router, then this will often configure itself automatically by looking for a DNS server on the external part of the network (which only it can see) and then act as a DNS relay whereby it pretends to be a DNS server for the internal network but instead passes all requests to the ISP’s DNS, before returning the results to you.

Having got an IP address of the DNS server (you’ll use the 192.168.1.1 of the router in this example), you can use the DHCP server to distribute this information to each machine when it also requests an IP address of its own. Because the same DNS server is used for all local machines, this can be done by setting the global option at the top of the /etc/dhcpd.conf file:

```
option domain-name-servers 192.168.1.1;
```

Alternatively, if you are not using DHCP to provide the networking credentials, then you must revert to the same /etc/network/interfaces file in which you specified its static address and add the following:

```
dns-nameservers 192.168.1.1
```

## Network Services

Having a machine on a working network is not enough to make one machine do something with another machine. Communication needs to take place. You’ve already seen two services in action (DHCP and DNS), and you’re probably aware of others such as HTTP to access web sites and FTP to transfer files. For your machine to work like this, you need to install a server of some kind. The trick is to know what kind of server is needed for any particular task. I will introduce these servers as needed. The first that I’ll show how to set up is a file-sharing server with the ability to provide files across the local network, allowing a musical collection to be situated on one machine but playable by any other on the subnet.

> **Note** It is possible to make files from the internal network available externally, but I’ll cover that later in this book.

The service that makes files available is called Samba, which allows files (and printers) to be shared between machines. Because it operates on a well-understood protocol (called SMB/CIFS), it can share these resources between different operating systems including Linux, Windows, and Mac OS X.^13

> [^13]: Version 10.2 and earlier.

It is installed in the usual way as your distribution, as shown here:

```
apt-get install samba
```

And it’s configured by editing this file:

```
/etc/samba/smb.conf
```

This is used to specify which folders on the local machine are available to the other computers and under what conditions, such as passwords or read/write privileges. Because the machine in question is on a private address range, the files will be accessible only to local machines, so you can generally make all these folders publicly accessible because in this context “public” means everyone in the house. Unlike a corporate network, abuse of networking facilities in a home environment (usually by the kids!) can be covered by not providing them with any dinner!

There are many ways of configuring Samba to provide files, but the defaults are good for a home environment.

I personally add sections to share various files in three specific ways. The first provides full access to my music and video files on my media server, such as /media/mp3. These are mounted in a directory structure like this:

- /media/mp3
- /media/tv
- /media/movies

and provided with the configuration section, like this:

```
[media]
comment = Media Server
path = /media
browseable = yes
public = yes
writable = no
read only = yes
guest ok = yes
```

This gives anyone at home, including visitors, a chance to listen to whatever band I’ve been enthusing about. It’s public (meaning my visitors don’t need a user account on my computer) and browsable (so it can be found on the network, without anyone knowing its exact name). However, it is made read-only, preventing visitors from accidentally (or maliciously, with rogue viruses perhaps) deleting the files.

They can see it from their Windows network neighborhood (or by typing `\\mediapc\media`) or from Linux (either by desktop or command line, with `smbmount //mediapc/media local_media_folder -o guest¹⁴`).

Next, I have a second share to the same location. This has a password, meaning that only I can add the latest DVD rips or music purchases to the system.

```ini
[media_incoming]
comment = Media Incoming
path = /media
browseable = no
public = no
writable = yes
read only = no
guest ok = no
```

The final share is my computer’s DVD drive. This is almost unused in my house because I’ve had the time to rip all my CDs and DVDs into files on my local machine, but it is still occasionally useful. The default installation provides a suitable example of the method here:

```ini
[cdrom]
comment = Media server's DVD
writable = no
locking = no
path = /dvd
public = yes
preexec = /bin/mount /dvd
postexec = /bin/umount /dvd
```

The last two lines will automatically mount the disk when asked for and unmount it after it’s been unused for a short period of time. The system is told how to handle the (un)mounting of `/dvd` with a suitable description in `/etc/fstab`:

```text
/dev/scd0        /dvd   udf,iso9660 user,noauto    0        0
```

Depending on the range and login configurations on your network, you may want to set up specific Samba users. If you’re a sysadmin by trade, setting up a centralized login database for all machines (Windows/Linux/Mac) might appear like a simple task. But for the rest of us, each machine will maintain its own set of usernames and passwords. Consequently, the Samba server has no way of knowing about these other machines or when their respective users decide to change their passwords. This makes it impossible for Samba to know what username/password combinations it should accept from this other machine. Therefore, it uses a separate set password table.

You simply need to type, as root, the following for each user who has password access to the particular Samba shared folders:

```shell
smbpasswd -a steve
```
