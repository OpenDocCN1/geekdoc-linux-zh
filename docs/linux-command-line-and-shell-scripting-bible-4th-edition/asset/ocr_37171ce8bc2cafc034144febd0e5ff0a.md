versions of the report to the current one to notify the script user of any differences between the two. Changes to file permissions indicate either new software was installed that needed these settings or that a file has been erroneously (or maliciously) set with these permissions. To perform this comparison, we can use the `diff` command. This utility allows us to compare files, and it displays any differences between the two to STDOUT.

# **WARNING**

The `diff` command compares files only on a line-by-line basis. Thus, for these reports it will compare line *1* of the first report to line *1* of the second report, line *2* to line *2*, line *3* to line *3*, and so on. If a new file or set of files is added, due to say a software installation, and the files need the SUID or SGID permissions, when the next audit is run, `diff` will display many differences! To solve this potential problem, you can use the *-q* or the *--brief* option on the `diff` command, and it will only display the message that the two reports are different.

We'll also need verification that another report exists before we try this comparison. Here's what this code looks like:

```
```
prevReport="$(ls -1t $reportDir/PermissionAudit*.rpt |
        sed -n '2p')"
#        if [ -z $prevReport ]
        then
            echo
            echo "No previous permission report exists to compare."
        else
            echo
            echo "Differences between this report and the last: "
            #    differences=$(diff $permReport $prevReport)
            #    if [ -z "$differences" ]
            then
```
```