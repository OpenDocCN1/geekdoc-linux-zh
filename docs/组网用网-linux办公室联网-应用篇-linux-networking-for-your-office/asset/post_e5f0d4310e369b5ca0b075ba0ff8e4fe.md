
## Note

Several versions of Linux's printer queue software have had buggy implementations of the rs feature. In Red Hat 5.2, for instance, the software treated all queues as if the rs option were enabled, whether or not it was specified in /etc/printcap. In Red Hat 6.0, lpd locks out all remote users when rs is set—even users with valid accounts on the server computer. At the time of this writing, Red Hat hasn't issued an official fix for this problem, although it is fixed in the lpr package that Red Hat is distributing with the betas for Red Hat 6.1. That fixed version is included in the sams-extras/printing directory of the CD-ROM that accompanies this book. If you need the rs capability, you should install this updated version of the lpr package.

- rg=—This option specifies a restricted group printer. For instance, if you specify rg=faculty, that printer will be accessible only to the faculty group. You can use this feature to restrict access to some arbitrary group of users. To do so, create a special group for printer access, add all the users you want to have access to that group, and add an appropriate rg= option to your /etc/printcap file.

It's important to realize that these features apply on a printer-by-printer basis. You can provide unfettered access to one printer, but restrict access to another on the same system. The rg= option also applies to users local to the server computer.

As an example of these two access control methods, consider the following sample /etc/printcap entry:

```
bigcolor:\n    :sd=/var/spool/lpd/lp:\n    :mx#0:\n    :sh:\n    :rs:\n    :rg=layout:\n    :lp=/dev/lp0:\n    :if=/var/spool/lpd/lp/filter:
```

This entry restricts access to the printer bigcolor to users who have accounts on the local system and who belong to the group layout.

## Tip

The rs option is only useful for restricting printing using native Linux/UNIX printer sharing mechanisms, but the rg= option can be useful with Samba, too. You can restrict printer access just as described here, and as long as your Samba users log on with their own passwords, you can restrict printer access in this way.

## Printing to a Remote UNIX Printer from Linux

Because native UNIX/Linux-style printing involves UNIX or Linux clients, it’s important to understand the client side of such printer configuration. For the most part, this configuration works much as described in Chapter 14, “Preparing to Share a Printer,” p. 351. There are a few unique details, though.

## Using printtool to Configure Printing

After you start printtool and click Add to add a printer queue, printtool asks what type of printer you want to add. Select Remote Unix (lpd) Queue and, instead of the Edit Local Printer Entry dialog box, printtool presents the Edit Remote Unix (lpd) Queue Entry dialog box, shown in Figure 15.1.

![](img/5d4d3092919d1d16884788127447cc6d_405_0.png)

### FIGURE 15.1

You must specify a remote host and printer queue when creating a local queue for a remote UNIX or Linux printer.

The Edit Remote Unix (lpd) Queue Entry dialog box works very much like the Edit Local Printer Entry dialog box described in Chapter 14. The only difference is that you must enter the name of the remote computer and the queue name of the destination printer on that computer, rather than the name of the printer device file. Other fields, including the printer name, spool directory, file size limit, and the input filter, work precisely as they do with local printers.

## NOTE

A printer queue can have one name on one computer and another name on another computer. For instance, the printer queue bigcolor on the print server fillmore might be accessed from the remote computer polk as epson1520. It's probably best for the sanity of all involved, however, if you attempt to coordinate printer queue names. If name conflict is inevitable (say, because multiple print servers have existing queues with conflicting names), try using a combination of the server and queue names as client computer queue names, as in fillmore_bigcolor or fm_bigcolor, to identify the bigcolor printer on fillmore. Alternatively, you might use the printers' locations in a similar way, as in fl2_bigcolor for the bigcolor printer on Floor 2.

## Configuring /etc/printcap Manually

An /etc/printcap entry for a remote printer queue is much like an entry for a local queue. As with a printtool-based configuration, you only need to alter the way the printer device is specified. Instead of an lp= option in /etc/printcap, you need to specify the rm= and rp= parameters to specify the remote system's name and the printer queue name on the remote system, respectively. For instance, here's a sample /etc/printcap entry for a remote printer queue:

```
bigcolor:\
:sd=/var/spool/lpd/lp:\
:mx#0:\
:sh:\
:rm=fillmore.threeroomco.com\
:rp=bigcolor:\
:if=/var/spool/lpd/lp/filter:
```

This queue directs input to the local bigcolor queue to a queue of the same name on the fillmore.threeroomco.com print server.

You can, of course, specify any access restrictions you want, remove the sh parameter to print a job separator page, and so on. These restrictions apply to jobs generated locally on your computer or accepted from a third computer by your system, but not to jobs sent to the print server directly from another source. Ultimately, it's the job of the print server's administrator to configure that system to print jobs in the desired fashion. If you administer several computers, though, you might want to spread the print queue handling around.
