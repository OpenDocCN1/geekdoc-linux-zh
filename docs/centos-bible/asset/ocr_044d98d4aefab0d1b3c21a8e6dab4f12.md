# **TABLE 11-2** *(continued)*

| Operator | What is Being Tested? |
| :--- | :--- |
| *file1* -ot *file2* | Is the first file older than the second file (using the modification time stamp)? |
| *file1* -ef *file2* | Are the two files associated by a link (a hard link or a symbolic link)? |
| *var1* = *var2* | Is the first variable equal to the second variable? |
| *var1* -eq *var2* | Is the first variable equal to the second variable? |
| *var1* -ge *var2* | Is the first variable greater than or equal to the second variable? |
| *var1* -gt *var2* | Is the first variable greater than the second variable? |
| *var1* -le *var2* | Is the first variable less than or equal to the second variable? |
| *var1* -lt *var2* | Is the first variable less than the second variable? |
| *var1* != *var2* | Is the first variable not equal to the second variable? |
| *var1* -ne *var2* | Is the first variable not equal to the second variable? |

# The case Command

Another frequently used construct is the *case* command. Similar to a *switch* statement in programming languages, this can take the place of several nested *if* statements. A general form of the *case* statement is as follows:

```
case "$VAR" in
    Result1)
        { body };;
    Result2)
        { body };;
    *)
        { body };;
esac
```

One use for the *case* command might be to help with your backups. The following *case* statement tests for the first three letters of the current day (*case* "`date +%a`" in). Then, depending on the day, a particular backup directory (BACKUP) and tape drive (TAPE) is set.

```
# Our VAR doesn't have to be a variable,
# it can be the output of a command as well
# Perform action based on day of week
case "date +%a" in
"Mon")
BACKUP=/home/myproject/data0
TAPE=/dev/rft0
```