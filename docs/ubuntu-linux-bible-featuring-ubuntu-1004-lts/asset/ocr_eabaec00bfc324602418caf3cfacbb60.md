# Chapter 25: Connecting to Other Systems

FIGURE 25-1

Verifying the state of the SSH server in the sysv-rc-conf Olivetti application

![](bbox=[0.063, 0.172, 0.578, 0.429])

# Connecting to Other Systems Using VNC

If you have multiple computers systems on a single network, getting up and going to the console of a specific machine to run a program quickly becomes old. You'd think there would be a way that a graphical computer system could connect to another graphical computer system over the network and display what you would see on that machine's screen a window on the first machine. Actually there is, and it's included in the standard Ubuntu distribution by default.

Virtual Network Computing (VNC) makes it easy for you to work on multiple graphical computer systems by enabling you to export their graphical displays across a network to another machine. VNC is a cross-platform technology originally developed by Olivetti Research Labs in Cambridge, England, which was later acquired by AT&T. A VNC server runs on one computer system and exports a desktop that can be accessed by a VNC client running on another system. VNC servers are typically password-protected, which makes VNC an optimal environment for accessing and running graphical administrative and monitoring applications. Remote VNC servers export their displays via network ports starting at 5900 plus the number of the graphical displays that they are exporting. For example, a VNC server running on the X Window display :1 will use port 5901.

VNC is released under the GPL, and many of the original VNC developers now work for a company called RealVNC (www.realvnc.com), which distributes and supports a commercial VNC implementation but also makes the source code for its version of the VNC server and client freely available, as required by the GPL. The latest generation of their VNC client is named