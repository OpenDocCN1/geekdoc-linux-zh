
commercial product. That core, instead of being a Linux kernel, is based on an open source project called Darwin (www.opendarwin.org).

Although Mac OS X and Linux are very different on the surface, there are many striking similarities. If you open a Terminal (shell) window on your Mac, you'll find that you can use many of the same basic commands that you can use from Linux. In addition, many of the same open source projects are included in both operating systems. These include:

- Samba (Windows file/printer server)
- Apache (Web server)
- CUPS (Linux print service)
- Sendmail (mail transport agent)
- BIND (DNS server)

There are also a few differences:

- Fedora is primarily covered under the General Public License, while OS X is based partly on an Open Source license and partly on a proprietary license. In August, 2003, APSL 2.0 was released (www.opensource.apple.com/apsl) and is now certified as a Free Software License from the Free Software Foundation.
- Fedora uses the Linux kernel; Mac OS X is based on the FreeBSD kernel.
- Most Linux configuration is done using system-config windows, which often create text-based configuration files (mostly in the /etc directory) from command-line or GUI applications; Mac OS X stores the configuration file in its own Netinfo database, which is manipulated primarily by GUI tools as well as by the `nutil` command.
- Fedora requires root permission for many administrative operations; OS X discourages overuse of the root login and encourages user accounts that are granted administrative privileges.

For the examples in this chapter, I used an iMac running Mac OS X 10.2.6. Because there were big improvements made between 10.1 and 10.2, I recommend that you upgrade your software if you are using the former. To see what version is installed on your Mac, open the Apple System Profiler from your Mac computer.

## Using Network Services from Mac OS X

You can easily connect your Mac OS X computer to your LAN by configuring the Network window. If Fedora is configured as a DHCP server (see Chapter 23), your Mac OS X client can detect that. Or, you can configure your LAN interfaces manually, as follows:

1. From the Dock bar, click System Preferences and select Network. This opens the Network window, which enables you to configure your network interfaces (see Figure 26-1).

![](img/b22364e57409c2481ba806e4e6b9309c_950_0.png)

Figure 26-1: Configure your Mac OS X network interface to connect to Linux servers.

2. If you are connecting to your Linux servers from a LAN, click the **Show** field and select **Built-in Ethernet**.

3. Click the **TCP/IP** tab. Then select either **DHCP** or **Manually** in the **Configure IPv4** field. If you select **Manually**, you can add the IP address of your computer, its netmask, the location of the router, the location of the DNS servers, and the domains to search. (For a home or small business, you might have a single Linux server serving as your router and DNS server. In this example, 10.0.0.1 is serving both of those functions.)

4. Click the **AppleTalk** tab. If you have configured your Linux server as an AppleTalk file and printer server (using netatalk), select the check box to turn on AppleTalk network protocols.

5. Click the **Proxies** tab. If you need to use a proxy server to access the Internet or other wide area network, use this tab to identify the proxies you are using.

The latest iMac computers have built-in Ethernet jacks that you can use to plug into your network hub. Plug your iMac into your LAN hub and you should be ready to use your Linux servers from Mac OS X.

## Using AppleTalk (netatalk) from Mac OS X

AppleTalk is the traditional set of protocols used by Apple computers to share files and printers over a LAN. Although Mac OS X can support Samba file sharing, AppleTalk is still a familiar way for Mac users to get to networked printers and files.

Inside Fedora is a software package called netatalk that you can use to configure Fedora as an AppleTalk file and printer server. To a Mac client, the netatalk server looks no different than any other AppleTalk server.

> **CROSS-REFERENCE:** Refer to the “Setting up the netatalk server” section later in this chapter.

To access a shared directory from an AppleTalk server, click Go in the Finder bar at the top of the screen, and then select Connect to Server. The Connect to Server window appears, as shown in Figure 26-2.

![](img/b22364e57409c2481ba806e4e6b9309c_951_0.png)

Figure 26-2: In Mac OS X, see Samba and AppleTalk shares from the Connect to Server window.

Enter the address, as shown in Figure 26-2, or click the Browse button to see a list of available servers.

After you click Connect, a pop-up window appears, prompting for a user name and password. Use the Options window to set up your preferences for logging on to the server. You can have the password added to your keychain so you don't have to type it in each time you access the server. You can also select to send the password in clear text (which is the default) and be warned that you are doing that. The server determines whether you need to enter a clear-text or encrypted password (so if you send the wrong type of password, it will fail). You can also request a secure connection over SSH for your login (which is a good idea to prevent someone from sniffing out your password from the network).

Figure 26-3 shows the Options window for selecting password options as just described.

![](img/b22364e57409c2481ba806e4e6b9309c_952_0.png)

Figure 26-3: Select authentication options when you connect to your AppleTalk (Netatalk) server.

After the user name and password are accepted, an icon representing the AppleTalk share appears on your desktop. Double-click to open the shared directory. You can change the contents of that directory in any way that your login will allow.

## Using AppleTalk from Mac OS 8 or OS 9

Prior to Mac OS X, Mac clients accessed AppleTalk shares from the Chooser window. The procedure for accessing a netatalk (or other AppleTalk) server went something like this:

- Click the Apple menu and select Chooser. The Chooser window appears.
- Click AppleShare. The file servers available on the local network appear in the Select a File Server window.
- Click the file server you want to access and click OK. You are prompted for a user name and password (or just presented with a guest login).
- Add the requested information and click OK. An icon representing the server appears on the desktop.

At this point, you can open the icon representing the shared directories and begin using the files and subfolders contained within.

## Using Windows and Linux servers (Samba)

The procedure for accessing Samba servers from your Mac OS X system is similar to the procedure for accessing an AppleTalk server from Mac OS X. As with the AppleTalk procedure, you open the Go menu from the Finder bar and select Connect to Server. From the Connect to Server window, do the following:

```
smb://ESTREET;christoys/toyprojects
```

Here are a few things you should know about accessing Samba shares from Mac OS X:

- When authenticating your password (see Figure 26-4), Mac OS X sends your password in clear text. Unlike when authenticating an AppleTalk share, there is no way to select to send encrypted passwords from this window.
- The example of setting up Linux Samba shares in Chapter 18 shows how to set up Samba to ask for encrypted passwords (and therefore will fail authentication from Mac OS X). To get around the problem (on a secure network), you can create a share that either accepts clear-text passwords or have the share be available to guest users.

> NOTE: To configure a particular Samba share to work from a Mac OS X client, you can edit the `/etc/samba/smb.conf` file (as root user). In a shared directory definition, add the line `guest ok = yes` (to allow guest users access to the share) or `encrypt passwords = no` to accept clear-text passwords.

## Sharing X applications

Most UNIX-like computer systems rely on the *X Window System* (also referred to as *X11* or simply *X*) to display graphically-based windows over a network. Sharing applications over the network with X requires little more than having X running and making it accessible to displays that are directed to your display (see Chapter 3 for information on launching X applications).

Although the default graphical interface for Mac OS X is a facility called Aqua, there is now an X11 for Mac OS X available for Mac users. The latest version of Mac OS X, nicknamed *Panther*, includes a native *X* installation. You must choose a Custom install or upgrade when you install Panther to get the X packages on your system. For further information on the state of the *X Window System* in Mac OS X, or to download your own copy of X11 for Mac OS X, go to `www.apple.com/macosx/features/x11`.

With X11 installed and running on your Mac OS X, you can launch X applications from your Linux system and have them appear on your Mac OS X desktop.

## Configuring an AppleTalk Server in Linux

If you have a mixture of older Macs (such as a Power Macintosh with Mac OS 8.1) and newer Macs (such as an iMac with Mac OS X) on the same LAN, an AppleTalk server could be the best way to share files and printers among them. With the *netatalk* package installed on your Fedora server, *netatalk* can be configured to act as that AppleTalk server.

Using *netatalk*, you can allow multiple Mac clients to use the following features from a computer running Fedora:

- **AppleShare file server** — Files and directories you share from your AppleTalk server (via *netatalk*) are stored with features and permissions that a Mac user would expect.
