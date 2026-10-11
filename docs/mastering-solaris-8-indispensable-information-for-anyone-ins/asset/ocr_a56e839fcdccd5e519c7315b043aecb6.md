# TABLE 10.1: LP PRINT SERVICE DIRECTORIES AND EXECUTABLE FILES (CONTINUED)

| Directory | Description |
|---|---|
| /var/spool/lp/logs | The logs directory is a symbolic link to the ../lp/logs directory, which contains the logs of completed print jobs. |
| /var/spool/lp/model | The model directory is a symbolic link to the /usr/lib/lp/model directory. |
| /var/spool/lp/request | The request directory is symbolically linked to the /usr/lib/lp/request directory. |
| /var/spool/lp/system | The system directory stores the print status file for your system. |
| /var/spool/lp/tmp | The tmp directory is a symbolic link to the /var/spool/lp/tmp/<printername> directory where spooled requests are stored. |
| /var/lp/tmp | The tmp directory has a subdirectory for each printer where print requests are logged. |
| /var/lp/logs/lpsched.n | The lpsched.n directory stores the daily files for the LP print log. |

Printer definitions are stored in the `printers` directory (`/etc/lp/printers`), which contains several files relating to individual printers. (If you don't have any printers set up, the `/etc/lp/printers` directory will be empty.) The printers directory contains the following files:

+   **alert.sh**   Stores the shell that is used when an alert is generated

+   **alert.var**   Contains alert variables used in conjunction with the shell when an alert message is generated

+   **comment**   Contains a description of the printer

+   **configuration**   Contains the printer's configuration information

+   **user.deny**   Stores a list of users who are prohibited from accessing this particular printer

When your system boots, the LP print service uses the `terminfo` database (`/usr/share/lib/terminfo`) to initialize local printers. The initialization procedure sends a set of control codes to the printer to set it up with the characteristics you have already specified: font, character set, form type, and so on.

The `lp` command takes input either as a filename or as text from standard output at the command line, then it creates a copy and places that copy in the appropriate spool directory. The `lpsched` daemon then schedules the print job by executing a print program or filter that formats the file and sends the appropriate control codes to the printer specified.