# Synchronise your files with Unison

# 05 Running Unison using a simple profile file

Some basic things you need to know about Unison profiles are:

- The default backup level is 2, which controls how many previous versions of each file are kept not including the current version of the file. So the default backup level keeps two backup copies of a file. This parameter for setting the backup level is called maxbackups.

+   * You can tell Unison not to keep file backups by not adding any backup options inside a Unison profile file.
+   * Unison profile files support Unicode characters.
+   * The log file option tells Unison to keep a log file called unison.log inside the .unison directory.
+   * Sometimes, network problems prohibit file synchronisation, but Unison's error messages are denoting the problem:

```
5 unison articles
Contacting server ... 
Connection closed by 109.x.x.y.y.zzz.
Fatal error: Lost connection with the server
```

# 06 Explaining the profile file

Lines starting with a # denote comments and are not processed any further. Exactly two lines must start with root = . They declare the machines (one is always the local computer) that are going to participate in the syncing process as well as the directories that are considered the root directories for each machine. After those important declarations, the actual directories that are going to be synced are listed. In this example we have just one directory (one path = line). Its full path is /Users/mtsouk/docs/article/working for the local machine and /home/mtsouk/docs/article/working for the machine called linode (an IP alias inside /etc/hosts). You can have as many path entries as you want. All files are synced except the ones that match the ignore option. You can also have as many ignore = lines as you want and can use regular expressions in them. The backup option tells Unison to keep backups of all files.

```
# Mihalis Tsoukalos
#
# Friday 05 July 2013
#
root = /Users/mtsouk
root = ssh://linode/home/mtsouk

# Paths to synchronize
path = docs/article/working

# Log file
logfile = /Users/mtsouk/.unison/unison.log

# Backup files
backup = Name *
ignore = Name *.DS_Store
ignore = Name .DS_Store
```

# 07 The .unison directory

Most of the Unison housekeeping happens inside the .unison directory which resides in the user's home directory. Unison keeps the following data there:

+   * Its profile files including the default profile called default.prf.
+   * Its backup files, if you decided to have central backups.
+   * The status file for each used profile.
+   * The Unison log file, should you tell it to keep one. You can put it anywhere you want but it is very convenient for it to reside there.
+   * Unison creates lock files there, during synchronisations, which it deletes when finished.
+   * Note It is not recommended to synchronize the whole .unison directory. Synchronising just the profiles is okay.

# 08 A more advanced Unison profile file

The contents of the advanced.prf file are as follows:

```
root = /Users/mtsouk
root = ssh://linode/home/mtsouk
times = true
batch = true

# Log file
logfile = /Users/mtsouk/.unison/unison.log

# Paths to synchronize
path = code/C

# Backup files
backup = Name *
backuplocation = central
maxbackups = 3
ignore = Name {Thumbs.db}
ignore = Name {.DS_Store}
ignore = Path {Samples.lnk}
```

![](bbox=[0.33, 0.73, 0.62, 0.95])

![](bbox=[0.63, 0.73, 0.92, 0.95])