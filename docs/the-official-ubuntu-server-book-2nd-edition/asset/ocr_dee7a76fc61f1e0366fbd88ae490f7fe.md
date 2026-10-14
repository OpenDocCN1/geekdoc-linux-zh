```
```text
'--times',
'--block-size=2048',
'--recursive',

    # my custom options
'--one-file-system',
];
$Conf{RsyncRestoreArgs} = [
    # Do not edit these!
    #
    '--numeric-ids',
    '--perms',
    '--owner',
    '--group',
    '-D',
    '--links',
    '--hard-links',
    '--times',
    '--block-size=2048',
    '--recursive',

    # my custom options
    '--one-file-system',
];
```
```

# Change the Backup Schedule

By default, BackupPC takes one full backup per week and in between takes an incremental backup of every host. BackupPC keeps one full backup and six incremental backups before it deletes anything. Finally, BackupPC will not start up new jobs for hosts that are always on the network between 7:00 a.m. and 7:30 p.m. during the week. These defaults are not suitable for everyone. For instance, you might be required to keep a month’s worth of full backups, or everyone might be out of the office by 6:00 p.m. so you can start backups then. All of these options are easy to change in the BackupPC Web interface.

To start, click the Edit Config link in the left sidebar and then click the Schedule link on the top right-hand side of the screen. You will see a schedule-editing screen as shown in Figure 7-5. The first set of options lets you schedule your full backups. Each of the options is hyperlinked to a manual page so you can read about what they change.

The FullPeriod option defines how much time should pass (in days) before a new full backup should be scheduled. This option is always set