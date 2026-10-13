to do this is to create a file in `/usr/local/etc/rc.d` that contains the command. Note that the file will need to be executable in order for the command to actually be run. (To do this, use the chmod command—for example, `chmod 655 myprintscript`.)

Now that you have configured the parallel port, you are ready to set up the printer’s spool directory, which is the directory on the hard disk where the printer stores print jobs waiting to be printed and also spools them to the printer.

# Configuring the Print Spool Directory

By convention, print spool directories are normally located in `/var/spool/lpd`. However, there is no rule that you have to put them here. Sometimes, you might want to put a spool directory somewhere else, such as if your `/var` partition doesn’t have enough space. For this example, we are going to assume that you are placing the spool directory in `/var/spool/lpd`. If this is not the case, simply replace this directory path with whatever directory you are putting the spool directory in.

The first thing you need to do is decide on a name for the printer. You can call the printer anything you want. Later, you can also create aliases for the printer that allow you to access it using other names. Aliases are covered later in this hour under the section “The /etc/printcap File.” If you have multiple printers in a large office environment, of course, it makes sense to name the printer something that either says something about what kind of printer it is, or where it is located. In this example, assume that we are configuring an HP Laserjet printer. So we will call it laserjet.

To create the spool directory for the printer, simply create a new directory in the `/var/spool/lpd` directory with whatever you have decided to name the printer. In this case, the following command will work:

```
mkdir /var/spool/lpt/laserjet
```

After you’ve created the directory, you will want to change the ownership and group membership so that they are both daemon and that only the user and group have any permissions on the spool directory. This will prevent users from snooping around the directory and looking at other people’s print jobs or possibly even deleting other people’s print jobs.

The following command will set the ownership, group membership, and permissions to their proper values:

```
chmod 770 daemon.daemon /var/spool/lpd/laserjet
```

After you’ve set up the directory, you need to configure a text filter for the daemon.