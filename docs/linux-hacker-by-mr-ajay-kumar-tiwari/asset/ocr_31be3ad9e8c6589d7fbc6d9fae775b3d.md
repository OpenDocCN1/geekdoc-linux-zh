# Linux Hack

/home/users/name_list.txt:John Doe

```
# grep -ril john /root
```

/home/users/subdir1/letter.txt

/home/users/name_list.txt

Ajay Kumar Tiwari

# Hack 18. Find Command

find is frequently used command to find files in the UNIX filesystem based on numerous conditions. Let us review some practice examples of find command.

Syntax: find [pathnames] [conditions]

# How to find files containing a specific word in its name?

The following command looks for all the files under /etc directory with mail in the filename.

```
# find /etc -name "*mail*"
```

# How to find all the files greater than certain size?

The following command will list all the files in the system greater than 100MB.

```
# find / -type f -size +100M
```

# How to find files that are not modified in the last x number of days?

The following command will list all the files that were modified more than 60 days ago under the current directory.