
## Networking and Internet Services
PART II

```
comment = All Printers
path = /var/pool/samba
browseable = no
printable = yes
# Set public = yes to allow user 'guest account' to print
public = no
writable = no
create mode = 0700
```

The comment, browseable, and create mode entries mean the same as those discussed earlier in the [homes] section. Note that browseable=no applies to the [printers] section, not to the printcap printers, which are listed in the SMB client's front end as a consequence of the [printers] section. If browseable=yes, a shared printers would be listed on the client. That's clearly what's needed.

The path entry indicates the location of the spool directory to be used when servicing a print request via SMB. Print files are stored prior to transfer to the printcap-defined printer's spool directory.

The printable value, if yes, indicates that this printer resource can be used to print. It must be set to yes in any printer share, including [printers]. The public entry controls whether the guest account can print. The writable=no entry ensures that the only thing written to the spool directory are spool files handled by printing functions.

## Samba Printer Troubleshooting Tips

Samba printer shares (including [printers]) usually work the first time. When they don't, it's important to remember a printer share won't work without a working Samba [global] section and remember a workingcap printer, and Samba won't work without a working network.

> Note
> The following troubleshooting tips work not only for the [printers] section, but also for any dedicated printer shares. Dedicated printer shares all have print ok=yes, and they have a printer name= option well.

Therefore, before troubleshooting any printer share including [printers], make sure the client and server machines can ping each others' IP address. If not, troubleshoot the network.

Next, make sure you can see the [global] defined workgroup in the client listing (Network Neighborhood or smclient -L Ipaddress). If not, troubleshoot Samba as a whole before working on the printer. Use testpartm (discussed later this chapter) to verify that smb.conf is internally consistent.

Next, make sure the printcap printer works properly. The printcap name can be deduced from the share's printer name= option. If there's no printer name= in the share, it can be deduced from the client request. Perform the following:

```
lpr -P printcap_printer_name /etc/fstab
```

This should print /etc/fstab to the physical printer defined as printcap_printer_name in /etc/printcap. /etc/fstab is an ideal test file because it's short and exists on all SuSE Linux machines. The machines can ping each other; the client can see the workday defined in the [global] section; and you can print to the printcap printer and are ready to troubleshoot the Samba printer.

Many Samba printer problems occur because the default samba printer command doesn't work. This is especially true if the printcap printer is a network printer instead of a local printer. First try putting the following line in the printer:

```
print command = lpr -P %p %s; rm %s
```

The command will print to %p (the printer name passed from the client) the file %s (the spool file passed from the client). You will notice this is the same command executed in the printcap printer tested previously, so it should work.

If it doesn't work, verify that the path=entry points to a directory to which the user has read and write access. Make sure any printer name=entry points to a working printer defined in /etc/printcap. Make sure the entry has a printable=yes or print ok=yes entry, it's not a Samba printer share. The printer share has a valid users= entry, make sure the user in one of those users.

If it still not working, it's time to install your test point. Temporarily create directory /home/freeall with mode 777 (all can read, write, and execute), comment out any print command= line in smb.conf, and add the following line:

```
print command = cp %s /home/freeall/%p.t; rm %s
```

This copies the file to be printed to a file in /home/freeall with the same filename as the printcap printer with the extension .t. This tells you which printer it's trying to print. First, the filename lets check /etc/printcap-printool for the existence of that printer. You can print that file and see if it comes properly.

If the file does not exist, you know something's on the wrong client of the side of printer command. Be sure to check the queue on the client to see if it's getting stuck. Sometimes single failure on the server can jam the client queue. Also be sure that all users can read, write, and execute directory /home/freeall; the print will otherwise bomb on permissions.

![](img/cbac72550c7126a22162e94d91a0c360_536_0.png)

After the problem is resolved, be sure to remove the /home/freeall test directory created for security reasons.

Another handy troubleshooting tool is checking the Samba logs. They usually contain useful error messages. If the log file is not defined in the [global] section of smb.conf, look in the /var/log directory. The two files are called log.nmb and log.smb.

Beyond these tips, remember that troubleshooting is a matter of keeping a cool head and narrowing the scope of the problem.

## Optimizing Samba Performance

Samba performs excellently, so performance usually isn’t an issue. If performance becomes an issue, there are several options to evaluate.

> Note
> The author tested all of the following Samba configuration performance enhancement techniques and was unable to attain any significant performance gains on an underloaded Samba server with a Celeron 333, 64MB of ram, a 7200rpm 14.4GB disk, and 100 Megabit/second wiring, using a test of copying an 11MB file back and forth. The conclusion is that gains depend on many factors, including but not limited to system load. These techniques will not help if the bottleneck is the wire, which appears to be the case on the author’s setup.

Samba performs excellently, so performance usually isn’t an issue. If performance becomes an issue, there are several options to evaluate.

> Note
> The author tested all of the following Samba configuration performance enhancement techniques and was unable to attain any significant performance gains on an underloaded Samba server with a Celeron 333, 64MB of ram, a 7200rpm 14.4GB disk, and 100 Megabit/second wiring, using a test of copying an 11MB file back and forth. The conclusion is that gains depend on many factors, including but not limited to system load. These techniques will not help if the bottleneck is the wire, which appears to be the case on the author’s setup.

Samba performs excellently, so performance usually isn’t an issue. If performance becomes an issue, there are several options to evaluate.

Samba performs excellently, so performance usually isn’t an issue. If performance becomes an issue, there are several options to evaluate.

Samba will follow all symbolic links even if they point outside share. Setting it to no gains some security benefits, disallowing access to these “outside of” links. However, further optimization may be gained by setting getwd cache= to yes in the [global] section. (The default is no.)

Tweaks to virtual memory utilization may also improve performance. If you are an advanced Linux user, you may be interested in trying them.

## Testing Your Configuration

After creating the configuration file, you should test it for correctness. Start by making the client and server can ping each others' IP address. Without a functioning network, Samba will not work.

Next use the testprogram. This is a simple test to check the /etc/smb.conf configuration file for internal correctness. If this program reports no problems, you can use the configuration file with confidence that smbd will successfully load the configuration file.
