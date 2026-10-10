# # Checking the Status of Print Jobs

Type: lpq OPTIONS USER.

The command's name comes from the fact that a spool is sometimes called a “queue.”

# ## The lpq Command (Print Jobs)

| Option | Action | Comments |
| :--- | :--- | :--- |
| -l | Print information for each file in the printer queue | |
| NUMBER | To check the status of a job number | |
| -P PRINTER | To set the printer that a job should use. | Not needed if the default is used. |

# # Removing Jobs From a Printer Spool

Type: lprm OPTIONS JOB USER.

The command's name comes from the fact that it removes (m) a job from a line printer (lp).

Only the root user can remove a job sent by another user. Regular users can remove their own print jobs.