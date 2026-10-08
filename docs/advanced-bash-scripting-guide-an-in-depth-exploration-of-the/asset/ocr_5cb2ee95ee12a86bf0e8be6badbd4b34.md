# Advanced Bash-Scripting Guide

Given a list of filenames, this script queries each target file (parsing the output of the file command) for the type of compression used on it. The script automatically invokes the appropriate decompression command gunzip, bunzip2, unzip, uncompress, or whatever. If a target file is not compressed, the script emits a warning message, but takes no action on that particular file.

# Unique ID

Generate a "unique" 6-digit hexadecimal identifier for your computer. Do not use the failed hosted command. Hint: md5sum /etc/passwd, then select the first 6 digits of output.

# Backup

Archive as a "tarball" (*tar.gz file) all the files in your home directory tree (/home/your-name) that have been modified in the last 24 hours. Hint: use find.

Optional: you may use this as the basis of a backup script.

# Checking whether process is still running

Given a process ID (PID) as an argument, this script will check, at user-specified intervals, whether the process is still running. Use the ps and sleep commands.

# Primes

Print (to stdout) all prime numbers between 60000 and 63000. The output should be nicely formatted in columns (hint: use printf).

# Lottery Numbers

One of lottery lists picking five numbers, in the range of 1 - 50. Write a script that generates five pseudonym numbers in this range, with no duplicates. The script will give the option of choosing the numbers to stdout or saving them to a file, with the date and time the particular number set was generated. (If your script consistently winning lottery numbers, then you can retire on the pennies and leave scripting to those of us who have to work for a living.)

# INTERMEDIATE

# Integer or String

Write script function that determines if an argument passed to it is an integer or a string. The function will return TRUE (0) if passed an integer, and FALSE (1) if passed a string.

Hint: What does the following expression return when $1 is not an integer?

```
expr $1 + 0
```

# ASCII to Integer

The atoi function in C converts a string to an integer. Write a script function that performs the same operation. Likewise, a shell script that does the inverse, mirroring the C atoi which converts an integer into an ASCII character.

# Managing Disk Space

List, one at a time, files larger than 100K in the /home/username directory tree. Give the user the option to delete or compress the file, then proceed to show the next one. To logfile the names of all deleted files and the deletion times.

# Banner

Simulate the printing of the deprecated banner in a script.

# Removing Inactive Accounts

Inactive accounts on a network server waste disk space and become a security risk. Write an administrative script (to be invoked by root or the cron daemon) that checks for deletes users accounts that have not been accessed within the last 90 days.

# Enforcing Disk Quotas

Appendix O. Exercises

844