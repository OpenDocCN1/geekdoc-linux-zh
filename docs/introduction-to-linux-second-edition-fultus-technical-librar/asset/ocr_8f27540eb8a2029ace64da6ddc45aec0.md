# **10.4.5 VNC**

VNC or Virtual Network Computing is in fact a remote display system which allows viewing a desktop environment not only on the local machine on which it is running, but from anywhere on the Internet and from a wide variety of machines and architectures, including MS Windows and several UNIX distributions. You could, for example, run MS Word on a Windows NT machine and display the output on your Linux desktop. VNC provides servers as well as clients, so the opposite also works and it may thus be used to display Linux programs on Windows clients. VNC is probably the easiest way to have X connections on a PC. The following features make VNC different from a normal X server or commercial implementations:

+   * No state is stored at the viewer side: you can leave your desk and resume from another machine, continuing where you left. When you are running a PC X server, and the PC crashes or is restarted, all remote applications that you were running will die. With VNC, they keep on running.
+   * It is small and simple, no installation needed, can be run from a floppy if needed.
+   * Platform independent with the Java client, runs on virtually everything that supports X.
+   * Shareable: one desktop may be displayed on multiple viewers.
+   * Free.

More information can be found in the VNC client man pages (man vncviewer) or on the VNC website <http://www.realvnc.com/>.

# **10.4.6 The rdesktop protocol**

In order to ease management of MS Windows hosts, recent Linux distributions support the Remote Desktop Protocol (RDP), which is implemented in the rdesktop client. The protocol is used in a number of Microsoft products, including Windows NT Terminal Server, Windows 2000 Server, Windows XP and Windows 2003 Server.

Surprise your friends (or management) with the fullscreen mode, multiple types of keyboard layouts and single application mode, just like the real thing. The man rdesktop manual provides more information. The project's homepage is at <http://www.rdesktop.org/>.

# **10.4.7 Cygwin**

Cygwin <http://www.cygwin.com/> provides substantial UNIX functionality on MS Windows systems. Apart from providing UNIX command line tools and