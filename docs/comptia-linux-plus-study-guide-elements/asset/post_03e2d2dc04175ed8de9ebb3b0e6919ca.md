
## Delivering Files Over the Network

### FIGURE 11.1 You must configure Web browsers to use a proxy server such as Squid.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_534_0.png)

Alternatively, you can use an iptables firewall configuration on your network’s router to redirect all outgoing Web traffic to the proxy server. (Chapter 9 describes iptables.) This configuration obviates the need to configure each client individually; however, it also means that if the proxy server corrupts data, your users will have no recourse. If you attempt such a configuration, be sure to exempt the proxy server computer from the rule, lest you set up an infinite loop in which the proxy server’s traffic is redirected to itself!

## Using Text-Based Web Clients

You’re probably already familiar with the most common Web browsers: GUI tools such as Mozilla Firefox, Konqueror, and Opera. A few text-based Web clients deserve mention, though: lynx, wget, and curl.

The lynx program is a text-based interactive Web browser. It has features that are similar to those of GUI Web browsers, but it doesn’t support graphics. You browse the Web with lynx by using your keyboard’s arrow keys to move a cursor from one link to another and then pressing the Enter key to select the link. Lynx is particularly useful if you need to browse the Web using a text-only display. Users with visual impairments also use lynx in conjunction with screen reader software.

The wget program enables you to retrieve a document from a Web server and store it locally—think of it as analogous to Linux’s cp command, but using a source document that’s a Web URL. For instance, suppose you want to retrieve the main page from the http://www.linux.org Web site. You could do so with the following command:

```
$ wget http://www.linux.org
```

In this case, *wget* will locate the main document (*index.html* in this case, although the filename could be different), retrieve it, and save it to disk. If you want to retrieve something other than the main page, you can specify its filename:

```
$ wget http://www.linux.org/apps/all/Administration/Backup.html
```

You can use quite a few options with *wget*; consult its man page for details. One option in particular deserves mention: *-r*, which causes *wget* to retrieve a site recursively—it copies the document you specify and all those documents from the same site that are referenced by it. This can be a handy way to back up the contents of a Web server from another computer, either because you maintain the site and need a local copy or because you want to retrieve a site for later offline reading.

The final text-mode Web command is *curl*. This tool is similar to *wget* in that it's designed to transfer files to and from computers. By default, though, *curl* displays the retrieved file on standard output, similar to *cat* for local files. This makes it handy for directly viewing text files retrieved from servers, but it's less useful than *wget* for backing up an entire site.

Although I've described *wget* and *curl* as Web retrieval tools, both support additional protocols. *wget* works with HTTPS (secure HTTP) and FTP, while *curl* works with these protocols along with TFTP, Telnet, and several others.

## Using Windows Remote Access Tools

Chapter 9 presented information on remote access using some common Linux tools, including SSH and the X Window System. These aren't the only remote access protocols available, however. A couple of tools are particularly useful for interoperating with Windows systems. The first of these is *rdesktop*, which uses the Remote Desktop Protocol (RDP) to connect to Windows systems that run Terminal Services to enable remote GUI logins. The second tool is Virtual Network Computing (VNC), which is a cross-platform GUI login tool that uses the Remote Framebuffer (RFB) protocol. You can configure a VNC server in Linux to enable logins from other systems, and you can use a VNC client to log in to remote systems.

### Using rdesktop

The *rdesktop* program is fairly straightforward to use, as you can see by its syntax:

```
rdesktop [options] server[:port]
```

Table 11.5 summarizes the most common *rdesktop* options. Consult the program's man page for a more complete list. Most of the options not shown in Table 11.5 are highly technical and relate to the way the protocol transfers data or to enabling the server to access local hardware devices on the client.

**TABLE 11.5 Common rdesktop Options**

| Command Name | Effect |
| :--- | :--- |
| -u username | Specify a username for accessing the server. |
| -d domain | Specify a domain for accessing the server. |
| -s shell | Start the specified program rather than Explorer on the server. |
| -p password | Pass the specified password to the server. This may have no effect if the Always Prompt for Password option is set on the server. |
| -g geometry | Specify the desktop size; geometry is specified as width and height, separated by an x, as in 1024x768. |
| -f | Enter full-screen mode. |
| -a bitdepth | Specify the color depth (8, 15, 16, or 24). Depths greater than 8 work only with Windows XP or newer. |

## Using VNC

VNC's greatest strength is its cross-platform nature. VNC clients and servers are available for Linux, other Unix variants, Mac OS, Windows, and more obscure OSs. This makes VNC a good choice for remote GUI access in a cross-platform environment.

### Configuring a VNC Server

The standard VNC server configuration on Linux is rather odd: it runs the VNC server as an ordinary user. Accessing the server produces a login to the computer as the user who ran the server. Thus, if Fred and Mary both run VNC servers on a Linux system, each can log in separately; but if George and Sally also have accounts on the system but don't run VNC, they won't be able to log in remotely. Behind the scenes, VNC server programs for Linux include both a VNC server and an X server; the two are linked, with the VNC server half functioning as a virtual keyboard, mouse, and monitor for the X server half.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_536_0.png)

It's possible to link VNC to an X Display Manager Control Protocol (XDMCP) server. When this is done, users who access the VNC server system will see a standard Linux XDMCP login screen. This configuration requires using advanced VNC options that aren't described here.

The first step to running VNC is to install it. Several different VNC servers exist, and most distributions ship with at least one of them. Typically, separate client and server packages are available, often called vnc and vnc-server, or variants of this (such as tightvnc and tightvncserver). If you're not sure whether VNC is installed on your system, use your high-level package manager, such as yum or apt-get, to search for relevant packages. If VNC isn't installed, install the appropriate packages for your distribution, or check the RealVNC Web site (http://www.realvnc.com) or the Tight VNC Web site (http://www.tightvnc.com). After you install VNC, follow these steps as an ordinary user on the VNC server system:

- 1. Create a directory called `.vnc` in your home directory. This directory will house your VNC configuration files.
- 2. Type `vncpasswd`. The program prompts you for a password and for a verification of this password. VNC doesn't, by default, use the normal Linux password database. You will need this password to gain entry to the system.
- 3. Type `vncserver`. This command is actually a script that performs various checks and then starts a VNC server (using the `vncs_program` file) in your name. The program displays some summary information, including a VNC session number:

```
New `tranquility.luna.edu:1` (neil) desktop is `tranquility.luna.edu:1`
```

You should now be able to access the VNC server system, as described in the upcoming section "Using a VNC Client." When you try this, though, you may run into problems. One common issue is that the server fails to start, or it starts and then crashes. Check for log files in `~/.vnc`. These files may include clues to the problem. One common problem relates to font paths; the VNC server is very sensitive about its font paths, and it will crash if you specify font directories that don't exist or that are misconfigured. You can add the `-fp` option and a comma-separated list of font directories to the command line to work around this problem. Alternatively, you can adjust your configuration files.

A second problem—or series of problems, really—is that various default options may be set strangely. Most configurations use two types of configuration files:

**The VNC Startup Script** The `vncserver` script includes within it various options, such as the default desktop size, the default font path, and so on. For the most part, these defaults are equivalent to X server defaults you would set in your local X server's `xorg.conf` file. You can edit this script to change these defaults.

**User Configuration Files** Most VNC servers use `~/.vnc/xstartup` as a user's local startup script. This script may call `/etc/X11/xinit/xinitrc` or some other local default startup script, or it may launch a bare-bones window manager, such as `twm`. In any event, you can edit this script much as you'd edit any other X startup script.

### Using a VNC Client

The Linux VNC client program is usually called `vncviewer`. This tool takes several options, but in most cases you use it by typing the program name followed by the VNC
