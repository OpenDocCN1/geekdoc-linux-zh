ditional parameters for how they get shared and how much of each one gets shared. Open up the Makefile with your favorite editor, and you can see all the configurable options. Let's step through the Makefile options that apply to NIS:

# ### Designating Slave Servers: NOPUSH

If you plan to have NIS slave servers, you'll need to tell the master NIS server to push the resulting maps to the slave servers. Change the NOPUSH variable to false if you want slave servers.

> > NOTE: If you don't need slave servers now but think you will need them later, you can change this option when you do add the servers.

```
```
# If we have only one server, we don't have to push the maps to the
# slave servers (NOPUSH=true); if you have slave servers, change this
to "NOPUSH=false" and put all hostnames of your slave servers in
# the file /var/yp/ypservers.
NOPUSH=true
```
```

Remember to list the hostnames of your slave servers in the /var/yp/ypservers file. And for each hostname you list there, be sure to list a corresponding entry in the /etc/hosts file.

# ### Minimum UIDs and GIDs: MINUID and MINGID

When accounts are added, the minimum UID and GID created in /etc/passwd and /etc/group files will be different depending on your Linux distribution. Be sure to set the minimum UID and GID values that you are willing to share via NIS. Obviously, you don't want to share the root entry via NIS, so the minimum should never be zero.

```
```
# We do not put passwd entries with lower UIDs (the root and system
# entries) in the NIS passwd database. For security. MINUID is the
# lowest uid that will be included in the passwd maps.
MINUID=500
# MINGID is the lowest gid that will be included in the group maps.
MINGID=500
```
```

# ### Merging Shadow Passwords with Real Passwords: MERGE_PASSWD

So that NIS can be used for other systems to authenticate users, you will need to allow the encrypted passwd entries to be shared through NIS. If you are using shadow passwords, NIS will automatically handle this for you by taking the encrypted field from the /etc/shadow file and merging it into the NIS shared copy of /etc/passwd. Unless there is a specific reason why you do not want to enable sharing of the encrypted passwords, leave the MERGE_PASSWD setting alone.