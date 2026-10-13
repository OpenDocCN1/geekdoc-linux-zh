+   - `/etc/protocols`: network protocol names and numbers
+   - `/etc/netgroup`: netgroup definitions
+   - `/etc/rpc`: remote procedure call program numbers
+   - Any other `/etc` files for which NIS maps are created.

For this reason, you need to copy these files from the old NIS master to the new one. Several options are available to do this, depending on your system and network configuration.

+   - Use FTP to transfer the files from one system to the other.
+   - Use NFS to mount `/etc` from one system to the other and then use the `cp` command to copy the files.
+   - Use the `rcp` or `rdist` command to copy the files between systems.
+   - Use the `tar` command to write the files to a floppy and transfer them to the new master.

# ## Deleting Time Stamp Files from `/var/yp` on the New Master

NIS generates timestamp files in `/var/yp` which are used to determine when data has changed. You need to delete any such files from the new master in order to force a database rebuild. These files all have `.time` extensions and can be deleted with the following `rm` command:

```
```shell
# rm -f /var/yp/*.time
```
```

# ## Running `make` with the NOPUSH=1 Option

Once the time stamp files have been deleted, you need to rebuild the NIS maps on the new master server. This will re-create the maps with the name of the new master server in them. The NOPUSH=1 option is used when generating these new maps so that the maps are not pushed out to the slaves automatically. This is necessary because the slave servers are still not ready to accept NIS maps from the new master server. To build the maps, change your current working directory to `/var/yp` and issue the following `make` command:

```
```shell
# cd /var/yp
# make NOPUSH=1
```
```

# ## Transferring the New NIS Maps from the New Master Server to the Old Master Server

You can force the transfer of NIS maps from the new master to the old master by using the `ypxfr` command on the old master server. If the hostname of your new NIS master server is `newmaster`, then the form of the `ypxfr` command is the following:

```
```shell
# ypxfr -h newmaster -f mapname
```
```

You will need to issue this command once for each NIS map. The complete list of NIS maps is outlined earlier in this chapter. If custom maps have been added at the local site, these will