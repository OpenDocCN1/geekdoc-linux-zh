
Once the system is up and running in single-user mode, if you supply the correct password, you will be superuser. If the system comes up in multiuser mode, you can log in as root, and again, if you have the correct password, you can be superuser. You can also give the `su` command while you are logged in as yourself. If you know the appropriate password, you will have superuser privileges.

> **TIP** If you use the official system version of `su`, always specify `su`’s absolute path name, such as `/usr/bin/su`, when you use it.

Many of the commands used by superuser are kept in the `/usr/bin` directory. You can execute these commands by giving their full path names on the command line or by including the `/usr/bin` directory in your `PATH` when you are logged in as superuser. You can also make changes to the console line in the `/etc/default/login` file and control where root is allowed to log in directly. No matter what is in this file, you can log in on the machine as an ordinary user and then use `su` to become root. This is a good setup for computers that are accessible to the public. With no root login available on the console, it will not matter if your machine is accessible. No one will be able to log in to the root account from the console. You will have to have a valid account on the computer before you can attempt to obtain superuser privileges. Change the line that begins with `CONSOLE` to read as follows:

```
# root cannot login directly on any device
CONSOLE =
```

If you are going to allow root to log in directly on the console, edit the `/etc/default/login` file and make sure the line beginning with `CONSOLE` is not commented out, as in the following example:

```
# root can log in on console
CONSOLE=/dev/console
```

If the machine is in a server room or a locked space where only trusted people have access to it, this type of access is permissible. However, even a server room should have additional physical security such as locked doors with coded key pads.

> **WARNING** Never allow root access over the Internet. If you comment out the `CONSOLE` line in the `/etc/default/login` file, you allow root to log in on the machine directly over the network, possibly by using Telnet. Do not allow this kind of root access to any machine connected to the Internet.

If you want to limit root login to a single port, use the following example:

```
# root can login only on /dev/term/a serial port only
CONSOLE=/dev/term/a
```

Almost everyone who deals with computers on any level has heard of the Trojan horse. Briefly, it is a program that appears to be innocent but does something either disruptive or destructive to your system. As a simple example, you could store the following program in a file called `tfile`:

```
while true
do
    echo 'You look terrible today! Out late again? Shame on you!' > /dev/console
done
```

If you were logged on as superuser and ran this command, it would continue to write the rather amusing message to the console. A disgruntled programmer could do much worse by simply changing superuser’s `PATH` variable to include a publicly writable directory at the start of the `PATH` string. Then they would need to put the bogus file in that directory. Because the bogus version appears in a directory mentioned earlier than the real one in `PATH`, the shell would run it. The next time superuser tried to run `tfile`, the bogus version would run. Although this is a simple example, Trojan horses have been known to create havoc in a computer system. When you log in as root, the shell will use `/etc/default/login`, but when you use `su` to become root, the shell reads the `/etc/default/su` script. Both scripts have a line that defines the variable `SUPATH`, which controls the value of `PATH` when you become superuser. Un-comment the line that begins with `# SUPATH` and change the value assigned to `SUPATH` there. Do not add `.` to `SUPATH` because you may set up a Trojan horse as described. The fewer directories you keep in your `PATH` when you are root, the less likely you will execute a bogus program as root. If possible, keep only the default `/usr/sbin` and `/usr/bin` directories. Remember, never include the working directory anywhere in the `PATH` string.

Leave the `/etc/hosts.equiv` and individual users’ `.rhosts` files empty. You can install products such as SKIP or IPsec, but they are somewhat complicated. Easier steps like preventing remote logins go a long way in keeping your host secure. Solaris does provide a number of utilities and packages for auditing host security setup. There is a three-level package called ASET, or Automated Security Enhancement Tool, that performs security auditing and detection. Process accounting can provide a continuous record of user actions on your system, but it will slow performance somewhat. If you have a large system, you may want to send important syslog information to a secure host that stores only syslog data. There are many good, free programs available for download from the Internet. Depending upon your system size, configuration, and number of users, there will be several suited to your needs.

## Remote Access Security

Like local login, remote logins need to be as secure as possible, even more secure considering the increased likelihood of illicit access. Again, you have to look at encrypted authentication clients such as STel, Kerberos, or Secure Shell (SSH), which are all discussed later in this chapter. Smart cards (discussed briefly later in this chapter) are an excellent choice for remote access login. Even if they inadvertently fall into the wrong hands, it is highly unlikely that the finder would be able to produce the correct response to a challenge.

The standard remote access tool for logging in to a Solaris computer is Telnet. A compiled client can be executed on operating systems that support the TCP/IP protocol. Any browser that runs Java natively or as a plug-in will support Telnet. Telnet is a terminal-like program that grants interactive access to a login shell of the user's choice. Most Telnet clients support VT100 or VT220 terminal emulations. This provides easy access to menu-based services. The login shell can be used to execute scripts. It can also be used to read e-mail, develop applications, or do anything a Solaris environment offers to its users. The one exception is graphics (X11, OpenWindows, CDE, and other graphical tools). A Solaris server may be located in a secure area of a site, with Telnet-only access allowed. Users never get to see the server or use CDE.

Once a request for a connection from the user to the server occurs, the server either responds or calls a timeout; if a timeout is called, a connection is either accepted or rejected. If the connection is accepted, the user is asked to enter a username followed by a password. If the username and password are valid, a shell is spawned and the user is logged in. Telnet does not encrypt your password or anything else. All data is sent as clear text across the network, making Telnet a very insecure way of logging on to a computer. This should be taken into account when logging on to Telnet. The standard port for a Telnet connection is 23. You can specify a port number on the command line.

Modems are a constant source of concern in remote security. Network lines are easily monitored. As quickly as folks come up with a new improvement to monitor security, hackers find new ways to get around it. Setting up an encrypted channel after dialing in to a modem pool is a good idea. This helps you to avoid being sniffed by the people running the dial-in pool, but it does not ensure the security of the pool.

You can do this by running SSH over PPP. Password Authentication Protocol (PAP) has stringent modem authentication policies that keep unauthorized users away from your modem. Challenge Handshake Authentication Protocol (CHAP) is also used frequently. They do not necessarily strengthen the security of the dial-in, but they make it easier to exchange data. One of the best and brightest, however, is RADIUS (sometimes called Steel Belted Radius). It tracks and documents all remote access activity and provides excellent authentication. Another good method of authentication is produced by Cisco and is called TACACS+. These are usually provided with Remote Access Service (RAS), which provides network access to remote users via modem.

If and when you purchase a remote access server, take a close look at what kind of security it provides and decide if that level of security is enough for your site. One technique employed by some remote access servers is callback. After you dial in, you will be prompted for a password. When you type in your password, the modem hangs up and calls you back at a phone number it has stored internally. If you have a small site with relatively few modems, this might work for you. It can be slow, however. Another technique is to use a caller ID (CLID) or automatic number identification (ANI) to decide whether or not to answer the call. You may or may not be able to use ANI, depending upon your local phone company and the type of wire it uses. ANI information is given before the call. CLID information is given along with the call.

If you have high-speed cable modem, look at security and authentication programs that are new and are compatible with the latest cable technology. The technology is changing rapidly and you'll want something with a bit of longevity.

You might consider setting up a virtual private network, or VPN. A VPN is a tunnel that shares a network infrastructure such as the Internet. It is a tunnel because the data being transferred is encrypted and then encapsulated in IP packets, protecting the sender's and recipient's identity. With today's technology, there are three principal ways to create VPNs:

- **Network to network** This is usually with a firewall or high-end router on each end of the VPN.
- **Host to network** A remote computer equipped with VPN client software can connect to the home office.
- **Dial-up ISP to network** Some ISPs will provide VPN service for clients.

VPNs can be used to connect a remote host to a network across the Internet if the client host is suitably configured. The firewall on each network is responsible for encrypting and encapsulating IP traffic that is then routed to the other network. When a user on one network needs to access a server on the other network, the firewall takes the workstation's IP packets and wraps them in its own IP packets. The packets that are then transmitted through the Internet contain source and destination addresses that
