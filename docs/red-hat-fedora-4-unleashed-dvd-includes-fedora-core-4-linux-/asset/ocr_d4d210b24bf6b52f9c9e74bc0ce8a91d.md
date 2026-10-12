the files referenced in the HTML, such as sounds, CSS files, and other related documents. You might also want to specify the -w parameter, which allows you to specify a number of seconds between individual wget requests; this stops your download from overloading the web server. So, the complete command to download a website (for example, www.example.com) would be `wget --mirror --convert-links -p -w 2 http://www.example.com/`.

# Using Graphical FTP Clients

Many graphical FTP clients are available for Linux. Fedora includes the graphical gFTP client and network-aware browsers included with GNOME and KDE. These browsers feature built-in drag-and-drop capability, thus ensuring FTP functionality. Other graphical interface clients that can be used for FTP include the Mozilla web browser, KDE's Conqueror, GNOME's Epiphany, and the Nautilus file manager.

# Using the gFTP Interface

The GNOME gFTP client provides all the typical features of FTP, including the ability to save profiles of common connections. Figure 22.1 shows a typical gFTP session in action. On the left panel is the local host, and on the right panel is the remote server. A connection is initiated by typing the address of the host into the host field, a specific port if not the standard FTP port (21), a valid username for the server, and a password. After the information has been entered, clicking the icon that looks like a monitor will start the connection to the server. The bottom panel displays session information, such as changing directories, as seen in Figure 22.1.

![](bbox=[0.19, 0.55, 0.81, 0.9])

FIGURE 22.1   A typical gFTP session.