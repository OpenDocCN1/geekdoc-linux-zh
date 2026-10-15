After you’ve edited these files, you can test diald by starting it. Type /usr/sbin/diald to start the daemon. If you don’t see any error messages, try a network access, such as ping www.linux.org. If diald is working correctly, your modem dials after a delay of a second or two, you connect to your ISP, and you start getting back responses from the ping command.
You can also use a Web browser, an FTP client, or other network applications. If you’ve configured your machine for IP masquerading, as described in Chapter 20, “One IP Address, Many Computers: IP Masquerading,” you should be able to use a computer on your LAN to initiate a PPP dialup connection, just by starting an appropriate Internet application and initiating a network transfer.

If you leave your computer idle for a while, so that it’s not transferring new data from the Internet, your modem connection should drop. The precise amount of time before this drop occurs is set in the file /usr/lib/diald/standard.filter, and varies depending on the type of the last transfer. For instance, Web transfers keep the link up for 2 minutes, whereas DNS requests without subsequent activity keep the link up for only 30 seconds. You can alter these settings by editing the standard.filter file. This file is well commented, so you shouldn’t have trouble finding the appropriate section for the type of transfer you want to affect. You specify times in seconds, so a value of 120 indicates a 2-minute delay before terminating the connection.

If you’re satisfied that diald is working correctly, and if you want it running constantly, you can add a line to /etc/rc.d/rc.local or some other initialization script to start it up when the computer boots.

# When to Use Dial-on-Demand

Compared to manual PPP dialing, dial-on-demand has unique advantages and disadvantages. Dial-on-demand’s strong points include the following:

+   - It is relatively transparent to users on a small intranet when PPP is the only connection type to the outside world.
+   - It requires no root access or special groups for dialout access. When the users on an intranet are served through IP masquerading, dial-on-demand doesn’t even require that the users have accounts on the dialing Linux box.
+   - It eliminates the possibility of online charges being driven up by accidentally leaving a link up for extended periods of time.

The weak points of dial-on-demand include the following:

+   - Delays when initiating a link can cause Internet applications to time out. For instance, if you start a Web access in a Web browser, the browser might report back that the site is unreachable before the PPP link has been established. You can generally just click a retry option or re-enter the address to start again, though.