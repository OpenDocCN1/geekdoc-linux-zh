```
next_id   = "lvm",
   title     = "Logical Volume Manager".
(Menu screen selected,
   FastPath   = "lv",
   id_seq_num = "020",
   next_id    = "lv",
   title      = "Logical Volumes".)
(Dialogue screen selected,
   FastPath    = "rm_lv",
   id          = "rm_lv",
   title       = "Remove a Logical Volume".)
[Jul 26 2001, 22:43:50]
   Command_to_Execute follows below:

   >> rm_lv -f 'paging00'

   Output from Command_to_Execute follows below:
   ---- start ----
   rm_lv: Logical volume paging00 is removed.
   ---- end ----
   [Jul 26 2001, 22:44:00]
```

# SMIT Script File

Along with the log file, SMIT appends the AIX commands invoked during the session to a local /home/smit.script file. The script file information can be used to create complex management scripts or review the commands invoked during a previous session. For example, say you use SMIT to configure the first of a set of 64 TTY devices. Edit the /home/smit.script file and, duplicating the mdev command 62 times for the remaining devices, change each device name and attributes as required. The script file can be executed from the command line to complete the definition for the remaining devices. Use the smit -s <PathName> option to create a script file in a location other than your home directory.

```
# smit -s /tmp/smit.script   Create a script file in /tmp
```

For example, the smit.script entries surrounding the removal of the paging00 paging space:

```
#       [Jul 26 2001, 22:43:50]
#
rm_lv -f 'paging00'
#
#       [Jul 26 2001, 22:44:23]
#
lsvg -o|lsvg -i -l
```