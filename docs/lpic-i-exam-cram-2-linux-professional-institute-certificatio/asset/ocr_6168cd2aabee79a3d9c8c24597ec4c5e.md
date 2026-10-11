472  Chapter 19

# Finding Files by Permissions

It's important to periodically run a `find` command to see which special bits are set on which files. To find all the files on your entire system that are owned by the root user with any special bit set and mail that list to yourself, you would use the following command:

```
find / -user root -perm +7000 -exec ls -l {} \; | mail -s
“Files that have any special bit set” root
```

This command finds the files that have any sort of special bit set, produces an `ls -l` listing from each, and sends an email that has the entire listing of files to the root user with the subject line in quotation marks.

When you use the `-perm` option with permissions, it matters whether you use a + or a - symbol or don't use one at all. If you are searching for a particular permission setting, such as all the files that have an exact permission setting, you would use the command shown here:

```
find / -perm 4777
```

This command finds only files whose permission trios and special bit match exactly the permissions specified. If you use the + and - symbols to search for special bits, the - symbol means to look for the exact combination of special bits that match the first numeral, such as 6, which would be 4 and 2—or SUID and SGID. To find any or all of the bits that are set that match the first numeral, you use the + symbol.

Once a week, run the same report again and then compare the first one with subsequent reports with the `diff` command to see what has changed. I'd suggest automating this with a script.

![](bbox=[0.09, 0.67, 0.21, 0.76])

> You'll probably see questions about the **find** command and the permissions, so be prepared to parse the commands to see which perform the specified tasks.

# Validating Package Integrity

Another important aspect of system security is to keep your systems up-to-date with the latest security patches and fixes. You should subscribe or follow the announcements from your distribution's vendor.

Keeping systems up-to-date is hard work, particularly if you do it by hand. However, most vendors offer some sort of automated update tool, the