```
Checking if /home/christine/sentinel file is empty...
The /home/christine/sentinel file exists and has data in it.
Will not remove this file.
$ 
```

First, the -f comparison tests whether the file exists. If it does exist, the -s comparison is triggered to determine whether the file is empty. An empty file will be deleted. You can see from the ls -sh command that the sentinel file is not empty (4.0 K), and therefore the script does not delete it.

# Checking whether you can write to a file

The -w comparison determines whether you have permission to write to a file. The can-I-write-to-it.sh script is simply an update of the can-I-read-it.sh script. Now instead of checking if you can read the item_name file, this script checks to see whether you have permission to write to the file:

```
$ cat can-I-write-to-it.sh
#!/bin/bash
# Check if a file is writable

item_name=$HOME/sentinel
echo
echo "Checking if you can write to $item_name..."
#
# Check if file exists and is a file.
# if [ -f $item_name ]
then
        # File does exist. Check if can write to it.
        # if [ -w $item_name ]
        then
            echo "Writing current time to $item_name"
            date +%H%M> > $item_name
        #
        else
            echo "Sorry, write access to $item_name is denied."
        fi
#
else 
```