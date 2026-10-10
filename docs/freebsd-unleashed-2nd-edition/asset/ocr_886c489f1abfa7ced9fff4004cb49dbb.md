All the same commands available in interactive mode are also available in noninteractive mode.

# Controlling Who Can Use 1pc

Sometimes you might want to give other people the ability to control printers with 1pc but not give them full root privileges on the system. The operator group allows you to do this.

Basically, any user who is a member of the group “operator” can make full use of 1pc without having full root access to the system. This will allow that user to change the priority of print jobs, start and stop print daemons, and bring queues up and down.

Refer to Chapter 9, “Users, Groups, and Permissions,” for more information on groups and how to add users to a group.

# Basic Network Printing

Basic network printing is similar to local printing. To set up a network printer in `/etc/printcap`, use a line like the following:

```
simba\lp|local line printer:\  :lp=::rm=nova:rp=simba:sd=/var/spool/lpd/simba:1f=/var/log/lpd-errs:
```

This entry will connect to a remote printer named simba on the host named nova. Note that the local name (on line 1) does not have to be the same as the remote name of the printer. You can call the local name whatever you want. What printer the job is actually sent to is controlled by the rp entry in line 2. The local spool directory will hold the file only until the remote spool directory has room. Then, the file will be moved into the remote host's spool directory.

Notice that we did not have to specify an input filter here. That is because all the filtering will be handled by the remote host.

The printer on the remote host should be configured using the instructions provided earlier in the chapter for configuring a printer.

> NOTE  CUPS (Common Unix Printing System) is an alternative to the 1pr system presented in this chapter. CUPS is intended to be a cross-platform printing solution for all Unix environments. CUPS is not a standard part of FreeBSD, nor is it included in a standard FreeBSD installation. It is, however, available in the FreeBSD ports collection under the print directory. For more information on CUPS, including documentation, visit the CUPS Web site at www.cups.org.