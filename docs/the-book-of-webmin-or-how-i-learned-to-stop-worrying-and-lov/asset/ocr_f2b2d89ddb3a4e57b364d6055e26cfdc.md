# PS command output style

This option should match the OS on which Usermin is running, as it chooses how to parse the output of the ps command. However, if your system uses a custom variant of this command, you may need to modify this to an OS that provides a similar ps.

# Cron Jobs

The Cron Jobs module allows users to create their own scheduled tasks to be performed automatically by the system at a specific time. The commands are performed with the permissions of the user that configured them.

# Crontab Directory

This should be set to the directory where cron looks for its crontab files.

# Command to read a user's cron job

Some crontab versions may use slightly different command line options, or you may use a special-purpose wrapper for cron. Here you can select the command and options for reading a user's crontab.

# Command to edit a user's cron job

Similar to the above Command to read a user's cron job, except it configures the command to edit a user's crontab.

# Command to accept a user's cron job on stdin

crontab can usually accept input from the standard input also, if the - pseudo-file name is given on the command line.

# Command to delete a user's cron jobs

This option sets the command Usermin will use to delete a user's crontab entries.

# Cron supports input to cron jobs

This option configures whether Usermin will provide a text entry box so that the user can provide data to the command being run via standard input. The command being run must accept data from standard input.

# Path to Vixie-Cron system crontab file

This should be the path to your system-wide crontab. Generally, it would be /etc/crontab.

# Path to extra cron files directory

Many systems make use of an extra cron directory for program specific cron jobs to execute when cron runs. This is likely /etc/cron.d.

# run-parts command

The run-parts command is often run in the system crontab file, and is used to specify other directories to run at specified times. For example, on a Red Hat Linux system the crontab contains: