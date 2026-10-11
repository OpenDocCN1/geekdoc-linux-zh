```
daemon /usr/local/samba/sbin/winbindd
```

in the example above with:

```
daemon /usr/local/samba/sbin/winbindd -B
```

The **stop** function has a corresponding entry to shut down the services and looks like this:

```
stop() {
KIND="SMB"
echo -n $"Shutting down $KIND services: "
killproc smbd
RETVAL1=$?
echo
KIND="NMB"
echo -n $"Shutting down $KIND services: "
killproc nmbd
RETVAL2=$?
echo
KIND="Winbind"
echo -n $"Shutting down $KIND services: "
killproc winbindd
RETVAL3=$?
[ $RETVAL -eq 0 -a $RETVAL2 -eq 0 -a $RETVAL3 -eq 0 ] && \
rm -f /var/lock/subsys/smb
echo ""
return $RETVAL
}
```

**Solaris** Winbind does not work on Solaris 9; see Section 41.6.2 for details.

On Solaris, you need to modify the /etc/init.d/samba.server startup script. It usually only starts smbd and nmbd but should now start winbindd, too. If you have Samba installed in /usr/local/samba/bin, the file could contains something like this:

```
##
## samba.server
##

if [ ! -d /usr/bin ]
then # /usr not mounted
```