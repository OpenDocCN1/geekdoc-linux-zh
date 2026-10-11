+   9. As with many devices, you need to use a lock file so that the print daemon is not trying to send multiple files to the printer while the printer is busy. Add this line in the format: `:lo=/var/spool/lpd/name/lock/name.lock:\`. In this case, you might use the following:
+   
+   `:lo=/var/spool/lpd/lp0/lock/lp0.lock:\`

+   10. This is it for the lines you must add for a local printer. Additional statements and arguments are laid out in Table 8.5. Be sure to end the last line in this print definition without the "`\`" component.

> **NOTE:** *You would use the pl or pw commands only if you were using something other than 8.5-by-11-inch standard letter-size paper.*

+   11. Press the Esc key and then type "ZZ" to save and close the file.

+   12. If you intend to print more than ASCII text, go to the section "Setting Up Popular Print Filters," later in the chapter.

+   13. Now you need to create the directories and files you are using. In the case of this example, these are as follows:
+       * `/var/spool/lpd/lp0`—The print spool
+       * `/var/log/lp0`—The error log file
+       * `/var/spool/lpd/lp0/lock/lp0.lock`—The lock file

> **NOTE:** *From here forward, change the directory and file names to match what you used.*

+   14. Type "ls /var/spool/lpd" to see whether this directory exists. If you get an error, continue with Step 15. If you don't, skip to Step 18.

**Table 8.5 Usefl /etc/printcap statements for setting up a local printer.**

| Type | Purpose | Example |
| :--- | :--- | :--- |
| mx# | Limits how large a print job can be, in K. A 0 means unlimited. The default is 1000, or 1MB. | mx#2000 |
| pl | Specifies how long (vertically) the page is, in lines. The default is 66. | pl=80 |
| pw | Specifies how wide (horizontally) the page is, in characters. The default is 132. | pw=150 |
| sh | Does not print headers at the beginning of every print job containing data about who printed the file. | sh |