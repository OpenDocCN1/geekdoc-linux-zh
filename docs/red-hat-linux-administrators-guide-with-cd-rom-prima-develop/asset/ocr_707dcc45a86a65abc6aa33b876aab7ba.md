Next, untar the downloaded file into a temporary directory, such as /tmp, or another directory over which you have the correct permissions. StarOffice should create an additional installation directory called so52inst\. Look for a file called setup:

```
#   cd /tmp/so52inst/
#   ./setup
```

Running this command as yourself or the appropriate user launches a graphical installation window. You will be prompted to fill out several forms that will include information about yourself as well as the configuration of your Internet connection. After you complete all the fields, StarOffice begins the install routine, a task that lasts only a few minutes depending on the speed of your computer. You should not need to tweak your system any further.

If you add StarOffice’s directory path either to the global /etc/profile file or to each user’s individual \_bash\_profile, you can start StarOffice from a single entry on a command line:

```
PATH="${PATH}:/usr/X11R6/bin:/usr/local/Office5.2"
```

Run the command *source* /etc/profile to enable the settings. StarOffice starts up with the simple command, *soffice*. To get your system fully functional on the Internet, StarOffice prompts you to fill out a few forms regarding your POP3 server, usernames, and the names of the servers that you frequent for connectivity. Filling out these forms is still a relatively minor task considering the ease and freedom that StarOffice grants in interfacing and exchanging information with other Microsoft systems and Microsoft-centric users.

Figure 12.6 shows how a regular text document appears along with the various menus that assist in choosing additional options. StarOffice emulates Microsoft to a high degree, so much so that it, too, along with the Start button, allows you to integrate the entire Linux desktop under the StarOffice display. This creates a Windows-like display. You may actually browse through the programs and directories under the StarOffice integrated desktop by pointing and clicking. Additionally, if KDE is already installed on the system, StarOffice detects this window manager and places a link on the KDE desktop, and also returns the *Fav* or incorporates all KDE programs into its own Start button. The smooth integration of these two systems can in part be credited to StarOffice’s own background as a German company, much like that of KDE’s own history with German developers.