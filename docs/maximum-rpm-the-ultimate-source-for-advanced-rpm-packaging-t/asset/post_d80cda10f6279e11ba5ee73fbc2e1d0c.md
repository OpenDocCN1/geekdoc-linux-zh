
### 20.4.3.2. Creating Uninstall Scripts

While there are install scripts, there are uninstall scripts. While there is no ironclad rule to that effect, it is a good practice. Following this practice, we have an uninstall script for the client package, and one for the server. Let's take the client first:

```shell
%postun client

# First, see if we're the last amanda-client package on the system...
# If not, then we don't need to do this stuff...

if [ "$1" = 0 ];
then
```

As before, we start out with a declaration of the type of script this is and which subpackage it is for. Following that, we have an if statement similar to the one we used in the install scripts, save one difference. Here, we're comparing the argument against zero. The reason is that we are trying to see whether there will be zero instances of this package after the uninstall is complete. If this is the case, the remainder of the script needs to be run, since there are no other amanda client packages left.

Next, we remove `bin` from the disk group:

```shell
# First, get rid of bin from the disk group...
if grep "disk:.*bin" /etc/group > /dev/null
then

    # Nuke bin at the end of the line...
    sed -e 's/\(^disk:[0-9]{1,}.*\),bin$/\1/' /etc/group > /etc/group.tmp

    # Nuke bin on the line by itself...
    sed -e 's/^\(^disk:[0-9]{1,}.*\),bin$/\1/' /etc/group.tmp > /etc/group1.tmp

    # Nuke bin in the middle of the line...
    sed -e 's/\(^disk:[0-9]{1,}.*\),bin\(,.*\)$/ \1\2/' /etc/group1.tmp > /etc/group2.tmp

    # Nuke bin at the start of the line...
    sed -e 's/\(^disk:[0-9]{1,}.*\),bin\(,.*\)$/ \1\2/' /etc/group2.tmp > /etc/group

    # Clean up after ourselves...
    rm -f /etc/group.tmp /etc/group1.tmp /etc/group2.tmp
fi
```

No surprises there. Continuing our uninstall, we start on the network-related tasks:

```shell
# Next, lose the amanda line in /etc/services...
# We only want to do this if the server package isn't installed
# Look for /usr/sbin/amdmp, and leave it if there...
if [ ! -f /usr/sbin/amdmp ];
then
    if grep "amanda" /etc/services > /dev/null
    then
        grep -v "amanda" /etc/services > /etc/services.tmp
        mv -f /etc/services.tmp /etc/services
    fi
fi
```

That's odd. Why are we looking for a file from the server package? If you look back at the install scripts for the client and server packages, you'll find that the one thing they have in common is that both the client and the server require the same entry in `/etc/services`. If an amanda server is going to back itself up, it also needs the amanda client software.

Therefore, both subpackages need to add an entry to `/etc/services`. But what if one of the packages is removed? Perhaps the server is being demoted to a client, or maybe the server is no longer going to be backed up using amanda. In these cases, the entry in `/etc/services` must stay. So, in the case of the client, we look for a file from the server subpackage, and if it's there, we leave the entry alone.

Granted, this is a somewhat unsightly way to see whether a certain package is installed. Some of you are probably even saying, “Why can’t RPM be used? Just do an `rpm -q amanda-server`, and decide what to do based on that.” And that would be the best way to do it, except for one small point: Only one invocation of RPM can run at any given time.

Since RPM is running to perform the uninstall, if the uninstall script were to attempt to run RPM again, it would fail. The reason it would fail is because only one copy of RPM can access the database at a time. So we are stuck with our unsightly friend.

Continuing the network-related uninstall tasks...

```shell
# Finally, the amanda entry in /etc/inetd.conf
if grep "amanda" /etc/inetd.conf > /dev/null
then
    grep -v "amanda" /etc/inetd.conf > /etc/inetd.conf.tmp
    mv -f /etc/inetd.conf.tmp /etc/inetd.conf
fi

# Kick inetd
if [ -f /var/run/inetd.pid ];
then
    kill -HUP `cat /var/run/inetd.pid`
fi
```

Here, we’re using grep’s capability to return lines that don’t match the search string, in order to remove every trace of amanda from `/etc/inetd.conf`. After issuing a HUP on inetd, we’re done.

On to the server. If you’ve been noticing a pattern between the various scripts, you won’t be disappointed here:

```shell
%postun server

# See if we’re the last server package on the system...
# If not, we don’t need to do any of this stuff...

if [ "$1" = 0 ];
then
    # Lose the amanda line in /etc/services...
    # We only want to do this if the client package isn’t installed
    # Look for /usr/lib/amandad, and leave it if there...

    if [ ! -f /usr/lib/amanda/amandad ];
    then
        if grep "amanda" /etc/services > /dev/null
        then
            grep -v "amanda" /etc/services > /etc/services.tmp
            mv -f /etc/services.tmp /etc/services
        fi
    fi
fi
```
