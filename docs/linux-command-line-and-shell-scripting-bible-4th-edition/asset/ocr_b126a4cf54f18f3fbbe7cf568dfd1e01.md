Sometimes, you don't want to install a file that is older than a file already installed on the system.

The -nt comparison determines whether a file is newer than another file. If a file is newer, it has a more recent file creation time. The -ot comparison determines whether a file is older than another file. If the file is older, it has an older file creation time:

```
$ cat check_file_dates.sh
#!/bin/bash
# Compare two file's creation dates/times
#
if [ $HOME/Downloads/games.rpm -nt $HOME/software/games.rpm ]
then
    echo "The $HOME/Downloads/games.rpm file is newer"
    echo "than the $HOME/software/games.rpm file."
#
else
    echo "The $HOME/Downloads/games.rpm file is older"
    echo "than the $HOME/software/games.rpm file."
#
fi
$
$ ./check_file_dates.sh
The /home/christine/Downloads/games.rpm file is newer
than the /home/christine/software/games.rpm file.
$
```

Neither of these comparisons in the script checks whether the files exist first. That's a problem. Try this test:

```
$ rm $HOME/Downloads/games.rpm
$
$ ./check_file_dates.sh
The /home/christine/Downloads/games.rpm file is older
than the /home/christine/software/games.rpm file.
$
```

This little example demonstrates that if one of the files doesn't exist, the -nt comparison returns incorrect information. It's imperative to ensure that the files exist before trying to use them in the -nt or -ot comparison.

# Considering Compound Testing