Now test it:

```
# /usr/local/atalk/bin/pap -p "LaserWriter 16/600
PS":LaserWriter@biology product.ps
```

If you are printing to a printer in your zone, you can leave off the name.

Assuming everything is working, the document should print out. Now you can go on to setting up /etc/printcap. Here is a sample entry:

```
lp|NetworkWriter|LaserWriter 16/600 PS:\n:sd=/usr/spool/laserwriter:\
:lp=/dev/null:\
:pl#63:\
:pw#85:\
:mx#0:\
:sh:\
:sf:\
:lf=/usr/adm/lpd-errors:\n:if=/usr/local/atalk/etc/filters/ifpap:\n:of=/usr/local/atalk/etc/filters/ofpap:
```

For more information on setting up remote and local AppleTalk printers see http://www.giub.unibe.ch/~eugster/appleprint.html.

# 5.5 Network Information Services (NIS)

The Network Information Services (NIS) is a set of programs for managing users and various network services from one master server. Recently an enhanced version of NIS, NIS+, is more secure, works better in large networks, but is more difficult to set up.

NIS began life the Yellow Pages. Yellow Pages however, is a registered trademark of British Telco so the name was changed. The original name legacy is still around, most of the programs associated with NIS begin with "yp."

NIS stores its information in a set of directories and GDBM (GNU Database Management) files rooted in /var/yp/F. NIS refers to these files as "maps.\ The maps are then made available to other machines in the NIS domain (not the same as a DNS domain!) via RPC (Remote Procedure Calls). NIS also allows for secondary slave servers. Slave servers get their maps from the master and answer requests if the master is slow or down, much the same way secondary DNS servers works.