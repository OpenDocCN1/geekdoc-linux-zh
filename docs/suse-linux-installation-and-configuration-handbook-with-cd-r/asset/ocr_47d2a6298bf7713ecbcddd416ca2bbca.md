+   6. Press Esc to go back to the dialing directory.
+   7. Press Dial. minicom will dial your ISP and bring up the login terminal.
+   8. Log in to your account.
+   9. After you have logged in, press Alt+Q to exit minicom without resetting the modem.
+   10. In the shell, start the pppd to pass control to it with the following command:
+       `bash#pppd`

To end the connection, start minicom again and issue the command ATZ, which will reset the modem. pppd will die and the connection will be terminated. You also can use `killall pppd` as root.

# Using kppp

If you like KDE and use it often, you will want to use kppp. kppp is a K application that features many capabilities (see Figure 23.10). Among them are multiple accounts, docking in the panel, modem lights, not needing to set up the /etc/ppp/options, accounting, and on-line graph activity. kppp configuration is performed using the dialogs that come up when you press setup. We will discuss the main dialogs and the connectivity procedures within kppp.

FIGURE 23.10
A screenshot of kppp.

![](bbox=[0.35, 0.62, 0.55, 0.78])

# The kppp Configuration Dialog

The kppp configuration dialog is the main configuration dialog from which the hierarchy of setting up your connection starts (see Figure 23.11). The Accounts tab enables you to configure as many accounts as you might have, along with their different ISPs, login scripts, and styles of accounting. The Device tab deals primarily with the serial port and its settings. The Modem tab enables you to set up your modem-specific commands (AT commands) and troubleshoot your modem via the modem terminal. The Graph tab enables you to activate the online graph. And lastly, the About tab provides information about the authors of kppp.

# The Accounts Tab

Setting up the accounts is very simple. Click New to make a new account, and then type in the connection name and phone number (see Figure 23.12). If you want to enter more than one phone number, separate the numbers with colons (:). Choose the type of authentication your ISP uses (for testing, use terminal-based). You can edit the pppd (PPP daemon) arguments by clicking the Arguments button. For more information on pppd arguments, refer to the section "Modifying the pppd Options" earlier in this chapter.