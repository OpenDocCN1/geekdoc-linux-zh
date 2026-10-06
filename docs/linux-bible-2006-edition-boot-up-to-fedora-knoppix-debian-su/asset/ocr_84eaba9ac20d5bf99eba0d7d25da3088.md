# 338 Part III ♦ Choosing and Installing a Linux Distribution

After you are done, click Next. SUSE sets up and tells you your network connections.

**18. User Authentication Method.** Normally, you will use your home computer in standalone mode, as it relates to user accounts. However, in a business setting, you may use NIS, LDAP, or Samba to get user account lists that allow access to yours and other computers on your LAN. If the latter is the case, select Client and choose neither NIS (a common facility used by UNIX systems to share configuration files) or LDAP (a standard directory service, used to share address books and other kinds of information on a network), depending on what your company supports. Choosing Samba lets you use Windows SMB file and print sharing features for authentication. Click Next.

**19. Add a New User** You will want to add at least one user account as prompted, for your computer. Right now you have the root user account set up for a standalone machine. Using that account for e-mail, Web browsing, or other common tasks is considered bad security practice: You should add at least one user account for non-administrative use of your computer. Add your full name, a one-word login name, and a password to protect that account. Click Next

When you are done, YaST writes the system configuration information to your computer. It displays the Release Notes for your current version of SUSE. Next to continue.

**20. Hardware Configuration.** You now have the opportunity to configure other hardware devices to use with your system. Select to configure your graphics card, printer, sound card, or TV card. After graphics configuration, you should test your display as prompted. If the settings don't work, select Ctrl-Alt-Backspace to exit and try to configure it again.

When you are done configuring hardware, click Accept. The settings are written to hard disk. An Installation Completed screen appears.

**21. Finish.** Click Finish. The system reboots and is ready for you to log in.

# Starting with SUSE

If you created a user account during the preceding installation, SUSE should automatically log you in as that user and present you with the KDE desktop. (If you are presented with a graphical login screen, log in as that user now). Here are a few things to help you get started using SUSE:

+   * **Desktop applications** The default SUSE 10.0 is installed as a desktop system that includes a set of easily accessible desktop applications. On the desktop, try the Office icon to open OpenOffice.org to work with documents, spreadsheets, presentations, drawings, Web pages, or a variety of other content types. From the SUSE icon on the panel, select from among dozens of applications to try out.