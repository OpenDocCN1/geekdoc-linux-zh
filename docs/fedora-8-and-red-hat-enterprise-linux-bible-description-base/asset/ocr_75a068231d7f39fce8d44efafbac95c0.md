+   - If you started the desktop by typing **startx** from your login shell, press Ctrl+Alt+Backspace to kill X and return to your login shell. Or you could type Ctrl+Alt+F1 to return to where you first ran **startx**, and then press Ctrl+C to kill the desktop.
+   - If you started the desktop from a graphical login screen (and Ctrl+Alt+Backspace doesn't work), first open a Terminal window (right-click the desktop and then select New Terminal). In the Terminal window, type `ps x | more` to see a list of running processes. Look for a command named gnome-session and determine its number under the PID column. Then type `kill -9 PID`, where *PID* is replaced by the PID number. You should see the graphical login screen.

Although these are not the most graceful ways to exit the desktop, they work. You should be able to log in again and restart the desktop.

# ## Setting Up an Online Desktop

As more and more services are moving off your desktop and on to the Internet, what features does the next generation of desktop systems need to be relevant? If the developers of the GNOME Online Desktop are right, the desktop will serve primarily as a tool for interconnecting your online services, applications, and friends.

The GNOME Online Desktop (http://live.gnome.org/OnlineDesktop) has been added as an experimental feature to Fedora 8. The centerpiece of the Project is an experimental sidebar called Big Board (http://live.gnome.org/BigBoard). From Big Board, you consolidate icons and menus to connect to your online photo services (like Flickr), retail accounts (such as Amazon), movie rentals (such as Netflix), and others. It also, however, keeps track of the files and applications you use locally.

You can use Mugshot (www.mugshot.org) to tie together connections to your online friends and activities. Mugshot lets you create the connections to your online accounts in a way that allows them to be used either from the Mugshot site or from your Online Desktop sidebar.

To get started with Online Desktop in Fedora 8, simply select Sessions → Online Desktop from the login screen. Then log in to Fedora with your user name and password. After that, you can set up online accounts with the Mugshot and GNOME projects. Then begin configuring the services you want on your Online Desktop. Type `yum install online-desktop*` to install Online Desktop.

The following steps take you through the setup of your Online Desktop:

+   1. **Change session** — From the login screen, select Sessions → Online Desktop.
+   2. **Log in** — Type your user name and password. A GNOME desktop configured with the Online Desktop feature appears.