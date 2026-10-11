are trying to see whether there will be zero instances of this package after the uninstall is complete. If this is the case, the remainder of the script needs to be run, since there are no other amanda client packages left.

Next, we remove bin from the disk group:

```
```
# First, get rid of bin from the disk group...
if grep "disk::.bin" /etc/group > /dev/null
then

# Nuke bin at the end of the line...
sed -e 's/(^disk:[0-9]{1,}\.\.{1,}\),bin$/\1/' /etc/group> /etc/group.tmp

# Nuke bin on the line by itself...
sed -e 's/^\(^disk:[0-9]{1,}.*\)bin$/\1/' /etc/group.tmp> /etc/group1.tmp

# Nuke bin in the middle of the line...
sed -e 's/(^disk:[0-9]{1,}.*),bin,(.\{1,}\)\(.*,\)2/ /etc/group1.tmp > /etc/group2.tmp

# Nuke bin at the start of the line...
sed -e 's/(^disk:[0-9]{1,}.*),bin,(.\{1,}\)\(.*,\)2/ /etc/group2.tmp > /etc/group

# Clean up after ourselves...
rm -f /etc/group.tmp /etc/group1.tmp /etc/group2.tmp
fi
```
```

No surprises there. Continuing our uninstall, we start on the network-related tasks:

```
```
# Next, lose the amanda line in /etc/services...
# We only want to do this if the server package isn't installed
# Look for /usr/sbin/amdmp, and leave it if there...
if [ ! -f /usr/sbin/amdmp ] ;
then

    if grep "amanda" /etc/services > /dev/null
    then
        grep -v "amanda" /etc/services > /etc/services.tmp
        mv -f /etc/services.tmp /etc/services
    fi
fi
```
```

That's odd. Why are we looking for a file from the server package? If you look back at the install scripts for the client and server packages, you'll find that the one thing they have in common is that both the client and the server require the same entry in /etc/services.

If an amanda server is going to back itself up, it also needs the amanda client software.

Therefore, both subpackages need to add an entry to /etc/services. But what if one of the packages is removed? Perhaps the server is being demoted to a client, or maybe the server is no longer going to be backed up using amanda. In these cases, the entry in /etc/services must stay. So, in the case of the client, we look for a file from the server subpackage, and if it's there, we leave the entry alone.