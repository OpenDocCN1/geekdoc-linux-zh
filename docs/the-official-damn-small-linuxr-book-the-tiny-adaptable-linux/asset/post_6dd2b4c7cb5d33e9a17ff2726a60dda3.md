
## Lua Applications

The developers of DSL are big fans of the programming language Lua (http://lua.org). We are currently using a build of Lua that has bindings to the Fast Light Tool Kit (FLTK), SQLite bindings, and networking capabilities.

This build of Lua was developed by John Murga and is aptly named murgaLua after the author. We take advantage of the GUI bindings to develop many tools, desktop utilities, and front ends for command-line applications, such as the DSL Control Panel and the MyDSL Manager.

Figure 3-11 shows a sample of tools that rely on murgaLua. Information about murgaLua may be found here: www.murga.org/devPages/murgaLua/index.html.

![](img/af53325d7f38f1cdafca9f44568e4ab8_86_0.png)

**FIGURE 3-11** DSL tools relying on murgaLua include dMix, MSDoc, Calendar, and Mount.lua.

Here is a short list of some of the tools found in DSL that rely on murgaLua.

### MS Word Viewer

This is a front end for the command line antiword Microsoft word viewer. With this application, you can select the .doc to view and pick whether you want to view the document as a PDF or PostScript.

### Calendar

This clever program, built on murgaLua and PSeal, can keep you organized. Calendar does a very nice job of formatting schedules, which get displayed in an easy-to-read calendar format.

### dMix

dMix is a GUI front end for the sound volume control umix. dMix is very simple to use and allows one to control the left and right side volume controls independently or sync them up for quick volume control.

### Mount.lua

This is a click to mount and unmount storage devices (floppy, CD-ROM, and disk partitions) in this GUI tool.

### Docked

The docked tool is used with Fluxbox, which incorporates much of the utility of dMix and Mount.lua.

## Daemon Applications

A daemon is a program that runs in the background waiting to be used upon request. Often daemons perform specific functions like remote connections, or printing.

Damn Small Linux is equipped with four daemons to help interact with the outside world. They are Open Secure Shell, NFS, BetaFTP, and the Monkey Web Server. Please note that all these daemon services are off by default and you need to enable them. Services may be controlled via the DSL control panel or the Fluxbox menu in the System, Daemons submenu. Also note that you have to set up a user password to remotely log in to a Damn Small Linux computer via either Secure Shell or FTP protocol.

### Open Secure Shell

Although it is standard on most distributions, many are surprised to learn that Damn Small Linux is equipped with an OpenSSH secure shell daemon. This makes it possible to securely access a remote computer running Damn Small Linux by logging in as user dsl or root. Using scp (a command-line utility to remotely transfer files between computers), it is also possible to securely transfer files into or out of Damn Small Linux remotely. Damn Small Linux has both the server and the client tools to do remote shelling and SCPing files around. Also, Damn Small Linux is equipped with a very handy utility, which allows one to remotely mount a file system via SSHD; the utility is called SSHFS, and we are big fans of it!

For information on OpenSSH, visit the manual page at www.openssh.com/manual1.html.

For more information on the SSH Filesystem, visit http://fuse.sourceforge.net/sshfs.html.

### BetaFTPD

BetaFTPD is an incredibly small (27K) single-threaded FTP server. Its small size made it a natural for Damn Small Linux, and its author, Steinar H. Gunderson, believes that being single threaded makes it more secure while also being easy on RAM. Yet, we mainly include BetaFTP for easy cross-platform file sharing when one does not have access to an SCP client.

For more information on BetaFTPD, go to http://betaftpd.sourceforge.net/.

### Network File System

As the name implies, network file system (NFS) is a system that allows one to share files across a network by remotely mounting disk partitions. It is similar in concept to the Windows file sharing system. Damn Small Linux has NFS-Common, which provides a tool set that allows you to use the NFS protocol.

Developer's note: In many ways, using SSHFS with Secure Shell can be used as an alternative to NFS. Many find it easier to use and more secure.

You can find an NFS howto page at http://nfs.sourceforge.net/nfs-howto/ar01s02.html.

### Monkey Web Server

Monkey Web Server is a simple and small web server, yet it is easy to configure and supports server side scripting. We include a get started page for Monkey as the default home page for localhost. To see it, just access the control panel and click the Monkey Web button, then point your web browser to http://localhost. The server files are located at /opt/monkey/ if you want to customize your setup.

The Monkey Web Server website can be found at http://monkeyd.sourceforge.net/.
