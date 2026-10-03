# Sourcing the Xsession.d Scripts

After sourcing the $HOME/.dtprofile script, the Xsession script sources the Xsession.d scripts. These scripts set up additional environment variables and start optional daemons for the user's session.

> CAUTION
Errors in any of the session startup files could prevent a user from logging in. To troubleshoot session startup problems, check the file $HOME/.dt/startlog. Session Manager logs each user's session startup progress in this file.

# Customizing the Welcome Message

After sourcing /etc/dt/config/sys.dtprofile (if it exists), $HOME/.dtprofile, and the Xsession.d scripts, Xsession displays a welcome message that covers the screen. You can customize the welcome message or turn it off entirely.

The dthello client is used to display the welcome message. To alter the message text, change the dthello options by modifying the dtstart_hello[0] variable. To change dtstart_hello[0], create a /usr/dt/config/Xsession.d script that sets the new value. For example, to display the message of the day for all users, create an executable sh or ksh script called usr/dt/config/Xsession.d/myvars, and set dtstart_hello[0] as follows:

```
dtstart_hello[0]="/usr/dt/bin/dthello -file \
/etc/motd &"
```

Users can also change the welcome message for their sessions by setting dtstart_hello[0] in $HOME/.dtprofile.

To turn off the welcome message, set dtstart_hello[0]=" ".

# Setting Desktop Search Paths

The desktop uses search paths, created at login, to locate applications and their associated desktop files. The desktop provides four search paths, described in Table B.2.

TABLE B.2
Desktop Search Paths

| Search Path | Description |
|---|---|
| Applications | Used to locate applications. Application Manager uses the Applications search path to dynamically populate its top level when a user logs in. |
| Database | Used to specify additional locations for action- and data-type definition files (*.dt files) and Front Panel files (*.fp files). |
| Icons | Used to specify additional locations for icons. |
| Help data | Used to specify additional locations for desktop help data. |

# Modifying a Search Path

# STEP BY STEP

# B.1 Modifying a Search Path

To modify the search path for a particular user, follow these steps:

+   1. Open $HOME/.dtprofile for editing.
2. Add or edit a line that defines and exports the personal input variable.