# **Table 7-1**
**Options Used with man**

| Option | Use |
| :--- | :--- |
| -C config-file | Specifies a config file other than the default of /etc/man.conf. |
| -M path | Specifies directories to search for man pages. |
| -P pager | Specifies the pager, or the program used to format and display the man pages. The default pager is specified via the PAGER environment variable. The more and less pagers are frequently used. |
| -S section-list | Specifies a colon-delimited list of man sections to search. |
| -a | Specifies that all matching entries are to be displayed, not just the first. |
| -c | Specifies that the source page is to be reformatted. |
| -d | Specifies that debugging information is to be displayed instead of the actual man pages. |
| -f | Specifies that man is to behave like the whatis program (discussed later in this chapter). |
| -h | Displays help information for the man command. |
| -k | Specifies that man is to behave like the apropos program (discussed later in this chapter). |
| -K | Searches the man page sources for the specified string. The user is prompted as to whether he or she wishes to view each entry found. |
| -m system | Specifies an alternate set of man pages to search based on the system name specified. |
| -w | Specifies that the path to man pages is displayed instead of the actual man page. |

An example of the use of the -a option follows. This causes the matching pages to be displayed in the order they are placed. The user is first presented with the crontab entry in section one. When the user hits the Q key to exit this man page, the entry found in section five is displayed.

```
```
# man -a crontab
```
```