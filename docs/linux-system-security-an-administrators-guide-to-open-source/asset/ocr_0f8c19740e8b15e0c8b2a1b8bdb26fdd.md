**Table 17.1 logrotate Configuration File Directives (Continued)**

| Directive | Action |
| :--- | :--- |
| postrotate/endscript | Commands between this pair of statements will be executed after the log is rotated. The *postrotate* and *endscript* keywords must each appear on lines by themselves, inside of *log rotation instructions* (they cannot be used as defaults). |
| prerotate/endscript | Commands between this pair of statements will be executed just prior to cycling of the log. The *prerotate* and *endscript* keywords must each appear on lines by themselves, inside of *log rotation instructions* (they cannot be used as defaults). |
| rotate *count* | Number of times to rotate files before they are removed. A 0 (zero) means remove the file rather than keeping an old version of it. A 4 would mean one current and four old copies of a file. |
| *size* *size* \| *sizek* \| *sizem* | Rotates files when they exceed a threshold of *size* bytes. You can also specify *sizek* or *sizem* to indicate kilobytes or megabytes, respectively. |
| tabooext [\+] *list* | By default, the list of extensions to ignore contains `.rpm-orig, .rpmave, v,` and `..` Set a new list of extensions to ignore by using tabooext *list* or add to it with tabooext \+ *list*. |
| weekly | Rotates log files on a weekly basis, usually the first day of the week. |

Table 17.2 shows command-line options that can be used with logrotate. As you can see from Table 17.2 logrotate is quite flexible. By default, logrotate expects to find the /etc/logrotate.conf configuration file. Example 17-1 shows a sample (with line numbers added for explanation purposes). We discuss the entries in /etc/logrotate.conf in the following sections.

**Table 17.2 logrotate Command-Line Options and Their Uses**

| Option | Use |
| :--- | :--- |
| -d | Debug mode. Read-only; no changes will be made to the logs or logrotate state file. |
| -f | Forces logrotate to run. This option is quite useful after new entries have been made. |
| -s *statefile* | Uses *statefile* instead of the default /var/lib/logrotate.status (allows multiple users to manage files). |
| --usage | Displays usage, version, and copyright information. |