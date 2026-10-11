+   4.  You are using tar to create a full backup of your system to a tape drive. Which of the following commands is your best choice?

+   a.  tar cvf mybackup.tar /
+   b.  tar cfb /dev/tape 20 /
+   c.  tar cvzfb mybackup.tar /
+   d.  tar cvzfb /dev/tape 20 /

Answer a is incorrect; this will create a tar file of your entire system but save it locally. Answer b is incorrect; this will write your tar file to the tape without compressing it. Answer c is incorrect; this would create the tar file and compress it but save it locally and not on the tape. Answer d is correct; this creates a compressed tar file on the tape containing all the files and directories of your system.

+   5.  You want to create a backup of your home directory to floppies, the total size of which is 2.1MB. After making your home directory your pwd, which of the following commands would be correct?

+   a.  tar cnfM /dev/fd0 1200 /home/*
+   b.  tar cnfM /dev/fd0 1200 /
+   c.  tar cnf /dev/fd0 1200 .
+   d.  tar cvf /dev/fd0 .

Answer a is incorrect; this would create a tar file of all the files in the /home directory, not just your files. Answer b is correct; this would create a multi-volume backup to 1.2MB floppies of the files and directories in the current directory. Answer c is incorrect; this would fail because your backup will not fit on a single floppy. Answer d is incorrect; you need to specify the size of the floppy and the fact that this is a multi-volume archive.

+   6.  You backed up your memos directory to mymemo.tar and now you need to restore the personne1.memo file. Which of the following commands will work?

+   a.  tar -xf mymemo.tar personne1.memo
+   b.  tar -xWf mymemo.tar personne1.memo
+   c.  tar -xw mymemo.tar personne1.memo
+   d.  tar -xn mymemo.tar personne1.memo

Answer a is correct; this will extract the file personne1.memo from the tar file mymemo.tar. Answer b is incorrect; the -W option verifies files after adding to a tar file. Answer c is incorrect; although this would place tar in interactive mode, it does not use f to name the tar file. Answer d is incorrect; the n option specifies that the device is just a tape.