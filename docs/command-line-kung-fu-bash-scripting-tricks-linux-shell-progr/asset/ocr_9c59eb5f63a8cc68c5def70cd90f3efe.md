```
```
three four
$ mount -t ext4
/dev/vda2 on / type ext4 (rw)
/dev/vda1 on /boot type ext4 (rw)
$ mount -t ext4 / ct
/dev/vda2 on / type ext4 (rw)
/dev/vda1 on /boot type ext4 (rw)
$
```
```

# **Grab the Last Word on a Line of Output**

```
```
$ awk '{print $NF}' file
$ cat file | awk '{print $NF}'
```
```

You can have awk print fields by using $FIELD_NUMBER notation. To print the first field use $1, to print the second use $2, etc. However, if you don't know the number of fields, or don't care to count them, use $NF which represents the total number of fields. Awk separates fields on spaces, but you can use the -F argument to change that behavior. Here is how to print all the shells that are in use on the system. Use a colon as the field separator and then print the last field.

```
```
$ awk -F: '{print $NF}' /etc/passwd | sort -u
```
```

If you want to display the shell for each user on the system you can do this.

```
```
$ awk -F: '{print $1,$NF}' /etc/passwd | sort | column -t
adm /sbin/nologin
```
```