```
echo "No differences exist."
else
    echo $differences
fi
```

Notice that checks are done not only for another report but also to see if there are truly any differences between the two reports. If there are no differences, only `No differences exist` is displayed.

# # Creating the script

Now that we have all the primary features figured out for this audit script, we can start putting it together. For this particular Bash shell script, we decided to use getopts (Chapter 14) and offer the use of the `-A` option to run only the account audit, and the `-p` option to execute only the permission audit. Although you can run both audits by combining the two options (-Ap), we included the flexibility of running both audits if no options were provided. This allows easier incorporation of this script into an automated environment via cron or anacron.

Here's the entire Audit_System.sh script for your review:

```
$ cat Audit_System.sh
#!/bin/bash
#
# Audit_System.sh - Audit system files and accounts
####################################################
#
### Initialize variables ####################
#
runAccountAudit="false"
runPermAudit="false"
#
reportDir="/home/christine/scripts/AuditReports"
#
### Get options (if provided) #################
#
while getopts :Ap opt
do
    case "$opt" in
        A) runAccountAudit="true" ;;
        p) runPermAudit="true" ;;
        *) echo "Not a valid option."
```