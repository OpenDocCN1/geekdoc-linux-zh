# EXPLANATION (CONTINUED)

4 The done keyword marks the end of this loop iteration.

5 When all of the users in the list have been sent mail and the loop has exited, this line is executed.

# EXAMPLE 14.34

(The Script)

```
#!/bin/bash
# Scriptname: backup
# Purpose: Create backup files and store
# them in a backup directory.
#
1 dir=/home/jody/ellie/backupscripts
2 for file in memo[1-5]
do
3 if [ -f $file ]
then
    cp $file $dir/$file.bak
    echo "$file is backed up in $dir"
fi
4 done
```

(The Output)

```
memo1 is backed up in /home/jody/ellie/backupscripts
memo2 is backed up in /home/jody/ellie/backupscripts
memo3 is backed up in /home/jody/ellie/backupscripts
memo4 is backed up in /home/jody/ellie/backupscripts
memo5 is backed up in /home/jody/ellie/backupscripts
```

# EXPLANATION

1 The variable dir is assigned the directory where the backup scripts are to be stored.

2 The wordlist will consist of all files in the current working directory with names starting with memo and ending with numbers between 1 and 5. Each filename will be assigned, one at a time, to the variable file for each iteration of the loop.

3 When the body of the loop is entered, the file will be tested to make sure it exists and is a real file. If so, it will be copied into the directory /home/jody/ellie/backup-scripts with the .bak extension appended to its name.

4 The done marks the end of the loop.