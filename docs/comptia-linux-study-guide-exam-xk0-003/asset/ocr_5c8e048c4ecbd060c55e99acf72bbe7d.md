message. To work around this problem, you must make an additional change, depending on how X is launched:

+   GDM On older versions of GDM, check the GDM configuration file (typically /etc/X11/gdm/gdm.conf); look for the line DisallowTCP=true, and change it to read DisallowTCP=false.
+   
+   On newer versions of GDM, edit /etc/gdm/gdm.schemas, and look for the line that reads <key>security/DisallowTCP</key>. A couple of lines below this, change the key from true to false.

+   KDM or XDM These two XDMCP servers both rely on settings in the Xservers file (in /etc/X11/xdm for XDM, and in this location or some other highly variable location for KDM). Look for the line that begins with :0. This line contains the command that KDM or XDM uses to launch the X server. If this line contains the string -nolistentcp, remove that string from the line. Doing so eliminates the option that causes X to ignore conventional network connections.

Special OpenSUSE configuration In OpenSUSE, you must edit /etc/sysconfig/displaymanager and set the DISPLAYMANAGER_XSERVER_TCP_PORT_6000_OPEN option to yes.

X launched from a text-mode login If you log in using text mode and type startx to launch X, you may need to modify the startx script itself, which is usually stored in /usr/bin. Search this script for the string -nolistentcp. Chances are this string will appear in a variable assignment (such as set defaultxserverargs) or possibly in a direct call to the X server program. Remove the -nolistentcp option from this variable assignment or program call.

Once you've made these changes, you'll need to restart X. Thereafter, X should respond to remote access requests.

![](bbox=[0.14, 0.69, 0.25, 0.78])

Distribution maintainers disable X's ability to respond to remote requests for a reason. If X responds to remote network requests, the risk of an intruder using a bug or misconfiguration to trick users by displaying bogus messages on the screen is greatly increased. Thus, you should disable this protection only if you're sure that doing so is necessary. You may be able to use an SSH link without disabling this protection.

Another option for running X programs remotely is to use the Virtual Network Computing (VNC) system (http://www.realvnc.com). VNC runs a special X server on the remote computer, and a special VNC client runs on the computer at which you sit. You use the client to directly contact the server. This reversal of client and server roles over the normal state of affairs with conventional X remote access is beneficial in some situations, such as when you are trying to access a distant system from behind certain types of firewall. VNC is also a cross-platform protocol; it's possible to control a Windows or Mac OS system from Linux using VNC, but this is not possible with X. (X servers for Windows and Mac OS are available, allowing you to control a Linux system from these non-Linux OSs.) Chapter 11 describes VNC in more detail.