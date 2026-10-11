# Table 11-6
Options Used with at

| **Option** | **Meaning** |
| :--- | :--- |
| -b | Allows jobs to be run when the system load is low. This is the same as the `batch` command. |
| -c job | Outputs the jobs listed to standard output. |
| -d | Removes an `at` job. |
| -f FILE | Used to specify a file containing the jobs that are to run. |
| -l | Lists all jobs for the user. |
| -m | Specifies that the user is to be mailed when the job completes. |
| -v | Shows the time the job is scheduled to run. |

The `at` command allows fairly complex time specifications. It accepts times of the form HH:MM to run a job at a specific time of day. If that time is already past, the next day is assumed. You can also specify midnight, noon, or teatime (4 p.m.), and you can have a time of day suffixed with AM or PM for running in the morning or the evening. You can also say what day the job will be run, by giving a date in the form *month day* with an optional year, or giving a date of the form MMDDYY or MM/DD/YY or DD.MM.YY. The specification of a date must follow the specification of the time of day. You can also give times such as `now` + `count time-units`, where the *time-units* can be minutes, hours, days, or weeks. You can also use `today` to run the job at a certain time today, and `tomorrow` to run the job tomorrow.

After entering the `at` command you will be given an `at` prompt where you enter the commands you wish to run. You can enter multiple commands here, which are run sequentially in the order listed. When you have finished entering commands, press Ctrl-D to save the job. This also saves the current environment including the directory and uses this information when the job is run. When running a job that has been saved to a file, include the correct paths so that the job will run correctly.

If you wish to control who has access to the `at` command on your system, you can use the `/etc/at.allow` and `/etc/at.deny` files. When checking for these files, the system first checks for the `/etc/at.allow` file. If this file does not exist, the `/etc/at.deny` file is checked. Because the `/etc/at.allow` file is checked first, if a user is listed there they will be allowed to run the `at` command regardless of whether they are listed in the `/etc/at.deny` file. It is a good idea to use either one or the other to manage your users’ rights with the `at` command. If you wish to allow all of your users to run the `at` command, simply empty the `/etc/at.deny` file. If neither `/etc/at.allow` or `/etc/at.deny` exists, only root is allowed to run the `at` command.