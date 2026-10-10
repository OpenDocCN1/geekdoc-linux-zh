+   2 Find files that belong to the group. Type: `find -l -group GROUP`. See “Searching for Files and Text,” page 167.

+   3 Change the group ownership on the files. See “Changing Groups,” page 225. To save effort, select multiple files.

# ## Editing a Group

+   1 Select the group. Logged in as root user, type: `groupmod -g GID`.

+   2 Find files that belong to the group. Type: `find -l -group GROUP`. See “Searching for Files and Text,” page 167.

+   3 Change the group ownership on the files. See “Changing Groups,” page 225. To save effort, select multiple files.

# ## Managing Printing

Linux includes a number of command line tools for administering printing. These commands are useful on networks, or for troubleshooting and managing printing on any system.

Each printer on a Linux system has its own spool or queue in the /var/spool/lpd directory. This spool uses the short name of the printer, which is created when the printer is first configured. When a file is printed, it becomes a job in the spool. Each job is stored in a spool until it is printed.

Printing tools generally start with lp (short for “line printer”). If you are familiar with other Linux commands, you can usually make a good guess at what the rest of the command should be. For example, lprm removes a print job from the spool

You can use the following tools for managing printing:

+   - lpq: Checks the status of print jobs.

+   - lprm: Removes a print job from a spool.

+   - lpstat: Reads the status of a spool.