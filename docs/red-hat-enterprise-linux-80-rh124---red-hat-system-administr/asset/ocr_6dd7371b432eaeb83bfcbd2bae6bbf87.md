Using the man command, research lp(1) to determine how to print any document starting on a specific page. Without actually entering any commands (because there are no printers), learn the syntax, in one command, to print only pages 2 and 3 of your PostScript file.

6.1 Use the man to determine how to print specific pages of a document.

```
$student@serverX ~$ man lp
```

> NOTE
From lp(1), you learn that the -P option specifies pages. The lp command spools to the default printer, sending only the page range starting on 2 and ending on 3. Therefore, one valid answer is lp passwd.ps -P 2-3.

7. Using pinfo, look for GNU Info documentation about the evince viewer.

+   7.1 Use the pinfo command to look for GNU Info documentation about the evince viewer.

```
$student@workstation ~$ pinfo evince
```

> NOTE
Notice that the evince(1) man page displays instead. The pinfo document viewer looks for a relevant man page when no appropriate GNU documentation node exists for the requested topic. Press Q to quit.