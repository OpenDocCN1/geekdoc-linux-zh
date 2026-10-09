![](bbox=[0.36, 0.1, 0.78, 0.3])

Figure 20-3 SquirrelMail running a configuration test

Startup You do not need to start SquirrelMail, nor do you have to open any ports for it. However, you need to configure, start, and open ports (if the server is running on a system with a firewall) for sendmail (page 743), IMAP (page 763), and Apache (page 936).

Configuration The SquirrelMail files reside in /usr/share/squirrelmail. Create the following link to make SquirrelMail accessible from the Web:

```
# ln -s /usr/share/squirrelmail /var/www/html/mail

```

Give the following commands to configure SquirrelMail:

```
# cd /usr/share/squirrelmail/config
# ./conf.pl
SquirrelMail Configuration : Read: config_default.php (1.4.0)

Main Menu --
1. Organization Preferences
2. Server Settings
3. Folder Defaults
4. General Options
5. Themes
6. Address Books
7. Message of the Day (MOTD)
8. Plugins
9. Database
10. Languages
D. Set pre-defined settings for specific IMAP servers
C Turn color on
S Save data
Q Quit

Command >>

```

This menu has multiple levels. When you select a setting (and not a submenu), conf.pl displays information that can help you decide how to answer the question it