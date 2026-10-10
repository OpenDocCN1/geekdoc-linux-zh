```
# /usr/share/squirrelmail/config/conf.pl
```

Features you might want to consider tuning include: Organization Preferences (such as the organization’s name and logo to put into the SquirrelMail interface), Themes (more than two dozen are available), and Plugins (just check whether any of those that are available to install are interesting).

Also, by default, mail can be accessed only from a browser on the local host, so you will probably want to change Server Settings. For example, change the Domain name to the name of the domain from which you will allow users to access their mail.

To use squirrelmail, users simply need to type the following address into the location box of their Web browser (replacing `server` with `localhost` or the name of the computer, if you are running this outside of the localhost):

```
http://server/webmail
```

Figure 18-1 shows an example of the webmail browser interface with the webmail logo replaced with the logo from my organization (in this case, LinuxToys net).

![](bbox=[0.128, 0.414, 0.82, 0.772])

**Figure 18-1:** Add a logo to SquirrelMail and let users log in from the Web to get mail.

Type your user name and password. Your mailbox should appear, as illustrated in Figure 18-2.