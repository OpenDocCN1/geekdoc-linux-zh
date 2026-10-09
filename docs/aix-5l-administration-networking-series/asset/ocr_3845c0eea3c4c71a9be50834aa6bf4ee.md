to select each software component to reject, or just enter ALL to reject all software in an APPLIED state.

# POST INSTALLATION AND MAINTENANCE TASKS

With the installation or maintenance process complete, there is still a bit of tidying up to be done before making the system available for use. A new installation requires that you set default system and environment variables. If you installed over an existing system, you will need to restore the previous environment. Product updates or maintenance will require testing before committing or rejecting the update. Finally, create new stand-alone media and take a fresh backup of the new system. A clean snapshot can be used as a reference point for installing additional machines or as a fallback should problems arise in the future.

# Review Install / Update Status

Review the status of software product and maintenance updates using List All Applied But Not Committed Software from the smitty installp menu or by invoking lsLpp from the command line.

```
# lslpp -h bos.rte
```

Display LPP history

```
Fileset Level Action Status Date Time
Path: /usr/lib/objrepos
bos.rte
5.1.0.0 COMMIT COMPLETE 07/26/01 17:52:34
Path: /etc/objrepos
bos.rte
5.1.0.0 COMMIT COMPLETE 07/26/01 17:52:34
```

LPP software can be in one of the following states:

+   - **APPLY** Fileset was being applied.
+   - **COMMIT** Fileset was being committed.
+   - **REJECT** Applied fileset was being rejected.
+   - **DEINSTALL** Fileset was being removed from the system.
+   - **CLEANUP** Fileset cleanup follows failed APPLY or COMMIT.

In the event of problems with the update, invoke cleanup and reinstall. LPP cleanup can be executed from smitty cleanup or via the installp -C option. Installations using