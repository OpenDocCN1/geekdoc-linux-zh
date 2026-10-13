FIGURE 10.8
The kppp client's PPP dialog box is used to determine how kppp should act depending on where you are in your X11 session.

![](bbox=[0.3, 0.15, 0.55, 0.42])

# Starting and Stopping PPP with kppp

To start your PPP connection, select your ISP from the kppp drop-down menu, and then click the Connect button (as shown in Figure 10.9). If you select the Show Log Window, a window appears as kppp attempts the connection. This is a handy diagnostic tool you can use to watch the progress and conversation between kppp and your ISP's computer. When the PPP connection is made, kppp docks into your desktop's panel as a small modem icon. The kppp client also makes temporary domain and name server entries in your OpenLinux system's /etc/resolv.conf file.

FIGURE 10.9
Click the Connect button in the kppp client's main dialog box to start a PPP connection.

![](bbox=[0.3, 0.7, 0.58, 0.85])

To get information about your PPP connection, right-click the modem icon on your desktop's panel, and then click the Restore menu item. A small dialog box appears with the name of your ISP. To view details about your connection, click the Details button, and a large dialog box appears, as shown in Figure 10.10.