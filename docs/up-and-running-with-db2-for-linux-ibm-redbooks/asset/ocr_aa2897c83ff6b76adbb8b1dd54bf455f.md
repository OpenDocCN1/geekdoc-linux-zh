# Table A-1 Commonly used command prefix sequences for db2_all and rah

| Sequence | Description |
|---|---|
| l | Runs the commands in sequence in the background. |
| l& | Runs the commands in sequence in the background and terminates the command after all remote commands have completed. |
| ll | Runs the commands in parallel in the background. |
| ll& or ; | Runs the commands in parallel in the background and terminates the command after all remote commands have completed. |
| < | Commands sent to all the machines for running except this one. |
| <<-nnn< | Commands sent to all other database partitions but not the database partition nnn for running. |
| <<+nnn< | Commands sent to only database partition nnn for running |
| > | Substitutes occurrences of <> with the machine name. |
| " | Substitutes occurrences of () by the machine index, and substitutes occurrences of ## by the node number. |

The first command in the following example shows you how to update database configuration parameters for all database partitions in the instance; and the second one shows you how to use prefix sequences for substitution purposes, and using the prefix sequence "'" (single quotation mark) to echo the commands that will be executed.

# Example: A-1 Using db2_all on a multiple partitions environment

```
$ db2_all "db2 update db cfg for sample using logprimary 10 logsecond 15"

DB20001I The UPDATE DATABASE CONFIGURATION command completed successfully.
UDBLNX06: db2 update db cfg for sample using logprimary 10 logsecond 15 completed ok

DB20001I The UPDATE DATABASE CONFIGURATION command completed successfully.
UDBLNX07: db2 update db cfg for sample using logprimary 10 logsecond 15 completed ok

$ db2_all "'">echo Machine Name: <> Partition Number: ##"
echo Machine Name: <> Partition Number: ##

Machine Name: UDBLNX06 Partition Number: 0
UDBLNX06: echo Machine Name: <> Partition Number: ## completed ok

Machine Name: UDBLNX07 Partition Number: 1
```