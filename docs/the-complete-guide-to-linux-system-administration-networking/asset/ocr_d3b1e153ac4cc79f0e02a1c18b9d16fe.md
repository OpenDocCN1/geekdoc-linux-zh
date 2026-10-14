The format of a printcap entry consists of a print queue name, followed by a series of 2-character option codes that apply to that printer. Each option is separated from the next by two colons. In the example file that follows, one of the colons is at the end of each line, and the second is at the beginning of the next line. Multiple options could be listed on a single line, so that you see two colons together; you see here a standard formatting method for this file. Many options are followed by specific parameters. For example, the parameter lp=/dev/lp0 specifies that the physical printer is connected to the first parallel port. For readability, each option is typically placed on a separate line of the file, with a backslash after each option to indicate that the line break should be ignored when processing the file. A basic printcap entry taken from Red Hat Linux is shown here:

```
local:\
:ml#0:\
:mx0:\
:sd=/var/spool/lpd/local:\
:af=/var/spool/lpd/local/local.acct:\
:sh:\
:lp=/dev/lp0:\
:lpd bounce=true:\
:if=/usr/share/printconf/util/mf_wrapper:
```

You learned in Chapter 3 how to create a basic printcap entry using the printconf-gui command in Red Hat Linux and Fedora. Other Linux distributions provide different graphical tools, such as Webmin or YaST. None of these graphical tools lets you set up all the possible options, but they usually get you started printing right away.

# Printing Remotely Using LPRng

When you defined a printer in Chapter 3, you created a "local" printer—one attached to your computer. You can also define a remote printer so that the lpd print server daemon sends print jobs to another computer instead of to a printer connected to your computer.

To do this, you define a printer on your system that refers to the remote computer and a print queue on the remote system. The lpd daemon on your computer communicates with the lpd program on the remote computer, transferring the print job. This arrangement is shown in Figure 12-12.

Once a print job has been sent to a remote system using lpd, you have no direct control over it. If you want to see the status of the print job, you must have permission to log in to the remote printer and use the printer management tools on that system.

Within the /etc/printcap file, a simple remote printer definition looks like this:

```
lp:\
:sd=/var/spool/lpd/lp:\
:mx#0:\
:sh:\
:rm=brighton.xmission.com:\
:rp=lexmark:
```