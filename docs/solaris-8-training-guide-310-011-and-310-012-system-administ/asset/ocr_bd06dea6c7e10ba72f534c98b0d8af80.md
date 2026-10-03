+   - Filters files (if necessary) so that they print properly
- Starts programs that interface with the printers
- Tracks the status of jobs
- Tracks forms mounted on the printer
- Tracks print wheels currently mounted
- Delivers alerts to mount new forms or different print wheels
- Delivers alerts about printing problems

Most of the LP configuration files are located in the /var/spool/lp directory, except for the interface files, which are located in the /etc/lp/interfaces directory. A SCHEDLOCK file should be in /var/spool/lp that is responsible for ensuring that only one instance of lpsched runs. You use the lpadmin command to add, configure, and delete printers from the system.

Information about printers can be found in the /etc/printers.conf file and files located in the /etc/lp directory. Solaris Admin tool provides a graphical interface to many of the lp commands listed in Table 10.2.

# TABLE 10.2

# SOLARIS lp COMMANDS

| Command | Description |
|---|---|
| accept/reject | Enables or disables any further requests for a printer or class entering the spooling area. |
| cancel | Lets the user stop the printing of information |
| enable/disable | Enables or disables more output from the spooler to the printer |
| lp | The user's print command. Places information to be printed into the spooler |
| lpadmin | Allows the configuration of the print service |
| lpmove | Moves print requests between destinations |
| lpsched | Starts the print service |
| lpshut | Stops the print service |
| lpstat | Displays the status of the print service |