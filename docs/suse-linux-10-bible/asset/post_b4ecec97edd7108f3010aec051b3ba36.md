
# Chapter 23 ♦ Running an FTP Server on SUSE 611

An anonymous FTP session looks something like Listing 23-3.

# Listing 23-3: Successfully Uploading Files

```
user@client: /home/user > ftp bible
Connected to bible.
220 (vsFtpd 2.0.2)
Name (bible:user): ftp
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd incoming
250 Directory successfully changed.
ftp> put afile
local: afile afile
229 Entering Extended Passive Mode (||62494)
150 Ok to send data.
226 File receive OK.
ftp> ls
229 Entering Extended Passive Mode (||50259)
150 Here comes the directory listing.
226 Transfer done (failed to open directory).
ftp>
```

Notice how the put command succeeds, but the ls command fails. As we planned, the anonymous login now permits uploads, but restricts directory listing. Further, the uploaded files cannot be downloaded by other users, so this is a fairly secure setup.

# Using pure-ftpd

The principles discussed in this chapter with reference to vsftpd apply equally to pure-ftpd, but there are some differences in detail.

You can set pure-ftpd to start in one of two ways: either as a service that starts at boot time or from xinetd as described for vs-ftpd.

If you choose the first method, you will need to edit the configuration file /etc/pure-ftpd/pure-ftpd.conf and then run the command rpure-ftpd start. To ensure that it starts at boot time, run the command chconfig pure-ftpd or use YaSt's runlevel editor. Despite the slightly confusing wording at the beginning of the configuration file, if you use this method the configuration file will be read when it starts, thanks to SUSE's init script.

# 612 Part IV ♦ Implementing Network Services in SUSE Linux

If you choose to run pure-ftpd over xinetd, it does not read its configuration file when it starts up. You need to edit the file /etc/xinetd.d/pure-ftpd to include a line

```
server_args = ...
```

To find out what to go after the = sign, you will need to run this command:

```
# /usr/sbin/pure-config-args /etc/pure-ftpd/pure-ftpd.conf
```

This parses the configuration file and converts the information in it to a long list of command-line switches that you can paste in. If you change the configuration file, you will need to repeat this process. For this reason, the first method of running pure-ftpd seems to be preferable, at least until you have created the configuration you.

# Further Information

You can find useful information in the comments in the configuration file /etc/vsftpd.conf, in the page for the configuration file:

```
man 5 vsftpd.conf
```

and under /usr/share/doc/packages/vsftpd/, including example configuration files for particular setups.

The home page for the vsftpd project is http://vsftpd.beasts.org/.

For pure-ftpd, there is also a man page (man pure-ftpd) and some documentation in /usr/share/doc/packages/pure-ftpd/. The home page for the project is at www.pureftpd.org.

Enough has been said in this chapter that you should think about whether or not you actually need to run an FTP server. FTP for users who have accounts on the machine is inherently insecure, and also unnecessary given the availability of ssh, scp, and sftp. If you need to run a server for files download, and the expected volume is not enormous, you may choose to offer those files by HTTP. If you want to run an anonymous upload server, check carefully that it is not open to any kind of abuse, and monitor its usage.

# Implementing Firewalls in SUSE Linux

# CHAPTER 24

## In This Chapter
- Using iptables
- Network Address Translation
- Redirecting traffic
- Using SuSEFirewall2

You have likely heard of a firewall before — your organization undoubtedly has one, and your asymmetric subscriber (ADSL) router probably has one, too. Linux has support for packet filtering (discussed later in the chapter) for quite a while now in some incarnation or another.

A firewall is a line of defense between two networks. It is used to explicitly allow network traffic to and from your networks, allowing you as an administrator to control what traffic can go where in your network. Many organizations not only use firewalls to protect their corporate network from the Internet, but also to protect one department from another. Is there any reason to allow the Sales department access to your Research and Development department? This also to slow the spread of a malicious user or virus code through your network if it is compromised because only explicit traffic or protocols can communicate with other networks.

Many companies provide firewall applications that offer the to use a graphical user interface to the firewall internals. With most asymmetric digital subscriber line (ADSL) routers, you also have the added bonus of a firewall. One of the most popular firewall applications used is the Cisco Pix. As with most things Cisco, it is at the business end of the market and knowledge of firewalls and how they work.

If you do not have a firewall solution at home or in the office, you can use an old PC to provide firewall services. A firewall does not need large amounts of memory or disk space because all the machine moves packets from one network interface to another while analyzing network information. Linux firewalls are bound by the speed of the processor. We have implemented a firewall server on an old Pentium 75 with 16MB of memory before, and it worked perfectly fine for a home network.

The first Linux firewall supporting came with the ipfwadm in the 2.0.x kernel series. With each major release of the kernel, the firewall code has been rewritten, with 2.2.x came iptchains, and the 2.4.x kernel brought us to iptables.

The Linux fireing, as we said, is packet filter-based. A packet filter will accept any network packet, dealing with the parameters that can be queried in the TCP/IP headers. For example, you can produce a rule that takes into consideration the source of the packet (the source IP address), the destination (destination IP address), the protocol (for TCP), the port (SSH), and the TCP options (SYN).

Taking all of these into consideration, you can define a rule that describes a very specific scenario for a network connection. Putting numerous rules together, you can produce a powerful firewall.

With the introduction of iptables, we were given the godsend that stately firewalls. iptables is something that most Linux administrators should know, especially when you need to secure your network or individuals machines from a network attack. They are relatively simple to use and extremely powerful when done correctly. All kudos to Rusty Russell (the lead iptables developer) for implementing this feature as it allowed us to produce firewalls with fewer rules.

# Why Use a Firewall?

A firewall, whether Linux-based or not, should always be used to protect machines connected to the Internet. A firewall, by its nature, is designed to control what can be accomplished over the network, and it is very unlikely that you 200 Windows machines be connected to the Internet in full view of any malicious person that comes along (and bare Windows machines on the Internet are like drops of blood in a 10-mile radius of a pack of sharks!).

Most people think that a firewall is there to stop crackers from the Internet, but the fact of the matter is that your users are trusted, it is all well and good to trust your users when you have security tests to see if they have a predisposition for breaking the rules you have imposed on them. However, internal situations are never always simple. Take the following example.:

We had a customer whose firewall was very tight at deterring Internet-based attacks and didn't let in anything that did not need to. For their internal users, there were no restrictions on connections to the Internet. All users were trusted and all good guys. Their email and operating systems on the other hand were not, and they started receiving emails with viruses that arbitrarily scanned
