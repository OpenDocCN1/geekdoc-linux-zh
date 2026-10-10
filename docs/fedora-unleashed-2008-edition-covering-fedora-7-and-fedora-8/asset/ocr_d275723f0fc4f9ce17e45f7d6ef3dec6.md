> **CAUTION**
> 
> Do not manually edit your `/etc/printcap`. Any changes will be lost when the printing service is restarted or if your system is rebooted. If you need to create customized printer entries, save the entries in `/etc/printcap.local` and then restart the printing service.

You can configure printing services using either the command line **system-config-printer-tui** program or the **system-config-printer-gui** graphical interface. Most of the detailed information in this chapter refers to the use of the GUI. The overview sections that follow, however, give you a solid foundation in both configuration approaches. You learn the details of these processes in later sections of the chapter.

# GUI-Based Printer Configuration Quick Start

Configuring a printer for Fedora is easy but you must use **root** permission to do it. Make sure that the **cupsd** daemon is installed and running. If you elect to use printing support when you install Fedora, the daemon and related software will be installed. If you're not sure whether **cupsd** is running, you can quickly drop to a terminal and use the **service** command with the name of the service and the **status** keyword like so:

```
# service cups status
```

You will see either

cupsd is stopped

or, if cupsd is running, an acknowledgement, along with its process ID, such as

cupsd (pid 2378) is running...

If **cupsd** is installed but not running, start the daemon like so:

```
# /etc/rc.d/init.d/cups start
```

You can also use the **service** command to start the daemon, like so:

# service cups start

If you are using the desktop, select System, Administration, Printing. You will be asked to enter the root password. If not, you are using X as root, which is a bad idea. Log out, and then log back in as a regular user! After you enter the root password, the printer configuration dialog appears.

You then simply follow the prompts to define your printer and add local or remote printing services. You should print a test page before saving your changes. Use the printer configuration client or the File menu's Print menu item from a GNOME or KDE client.