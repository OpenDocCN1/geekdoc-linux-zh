# Table 25-5: (continued)

| Comparison | Description |
|---|---|
| -f file | Checks if file exists and is a file |
| -r file | Checks if file exists and is readable |
| -s file | Checks if file exists and is not empty |
| -w file | Checks if file exists and is writeable |
| -x file | Checks if file exists and is executable |
| -O file | Checks if file exists and is owned by the current user |
| -G file | Checks if file exists and the default group is the same as the current user |
| file1 -nt file2 | Checks if file1 is newer than file2 |
| file1 -ot file2 | Checks if file1 is older than file2 |

These conditions give you the ability to check files in your filesystem within your shell scripts, and are often used in scripts that access files. The -e comparison allows you to check if a file or directory object exists before you attempt to use it in your script:

```
$ cat test19
#!/bin/bash
# checking if a directory exists
if [ -e $HOME ]
then
echo "OK on the directory, now let's check the file"
# checking if a file exists
if [ -e $HOME/testing ]
then
# the file exists, append data to it
echo "Appending date to existing file"
date >> $HOME/testing
else
# the file doesn't exist, create a new file
echo "Creating new file"
date > $HOME/testing
fi
else
echo "Sorry, you don't have a HOME directory"
fi
$ ./test19
OK on the directory, now let's check the file
Creating new file
$ ./test19
OK on the directory, now let's check the file
Appending date to existing file
$
```