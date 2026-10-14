defines what hour or fraction of an hour the blackout period begins, and the hourEnd option sets when it ends. The weekDays option sets which days of the week the blackout period is in effect. By default the blackout period is between 7:00 a.m. and 7:30 p.m. Monday through Friday.

To demonstrate how you would change these options, I define a different backup policy that might be used in an organization. In this organization we want weekly full backups and daily incremental backups, but we want to save the full backups up to a month before discarding them. We also want to keep the last two weeks of incremental backups. Finally, everyone in the office leaves by 6:00 p.m., so we want to start backups then. To make these changes I need to change only the following values:

```
FullKeepCnt = 4
IncrKeepCnt = 12
hourEnd = 18
```

# Restore Files

Backing up files is all well and good, but it isn't too useful unless you can restore them. One of the best features of BackupPC in my opinion is its easy-to-use Web-based restore. If you set up additional Web accounts for backuppc (use htpasswd -c /etc/backuppc/htpasswd username), you can add those accounts to specific hosts in the /etc/backuppc/hosts.conf (or on the Web interface) and those users can log in to BackupPC and restore their own files.

To restore a file or directories for a host, first go to the host's home page on BackupPC (select the host in the drop-down menu in the left sidebar). On the host's main page you will see a list of completed backups in a table that lists whether the backup was full or incremental, when the backup started, how long it took, and where those files are stored on the file system. Click the hyperlinked backup number at the beginning of a particular row to restore from that backup. You will then see the entire directory structure of your host on the page with checkboxes next to files and directories (Figure 7-6). The interface is like that of most file managers, and you can click on an individual directory to expand it. Once you have selected all of the files you wish to restore, click the "Restore selected files" button at the top or bottom of the page.