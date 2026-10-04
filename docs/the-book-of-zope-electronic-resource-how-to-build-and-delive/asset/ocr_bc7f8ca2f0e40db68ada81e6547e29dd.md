We'll select the format "SHA," which provides the best security.
Next, the Domain Restrictions query appears. For this option, you can specify a domain from which you can have direct access to the Zope Management screen. Leave this option blank (to allow access from all domains) and press RETURN.

Domain restrictions:

Give the "root" user access to all files in the /Teserver directory.

# 1.5.3.5 Access Permissions

Change to the directory /usr/local/ZopePark and enter the following:

```
chown -R root.root Teserver
```

The var and access directories must be given different access permissions.
Change to the Teserver directory and enter the following:

```
chown -R nobody.nroup var
chown -R nobody.nroup access
```

The Zserver is started and stopped using a start script called start and a stop script called stop. These scripts are located in the Teserver directory.

# 1.5.3.6 Assign IP Addresses

You now need to assign an IP address to the Zserver, because you will no doubt want to access your Zope server using a specific WWW address at a later stage (for example, www.mycompany.com). To do this, either you or your ISP will need to enter this WWW address and the associated IP address in the name server entries.

For example, assume our web address is www.mycompany.com and our allo-cated IP address is 212.11.222.333. To assign this IP address to the Zserver, you'll need to make a number of changes to the start script, as discussed below.

# Start Script

The start script should look like this at present:

```
#! /bin/sh
reldir= dirname $0
PYTHONHOME= cd $reldir; pwd
Export PYTHONHOME
Exec /usr/bin/python \
$PYTHONHOME/z2.py \
-D "$@"
```