+   1 In the GNOME Control Center, select the box beside Use "procmail" for local delivery on the System > Electronic Mail pane.

+   2 Create a text file called .procmailrc in your home directory. See “Lines in the .procmail File,” page 391.

+   3 If necessary, create the directory in which to filter mail. This directory can be one created and used by another mailreader.

+   4 Create a sub-directory in your home directory called .procmail to hold procmail files.

+   5 Create filters. Place each filter in a file called rc.FILTER in the .procmail directory. See “Filters for procmail,” page 392.

+   6 Create a file called .forward in your home directory. This file activates procmail when new mail arrives.

In the .forward file, enter:

```
"IFS='\| ' exec /usr/bin/procmail -f || exit 75 #user"
```

![](bbox=[0.1, 0.5, 0.16, 0.53])

> Note
> 
> For examples of .procmail files and more ideas of what you can do with them, see the sample files in the /usr/share/docs/procmail/examples directory.

# Lines in the .procmail File

| Line | What It Does |
| :--- | :--- |
| PATH= /usr/bin | Defines the location of the utility. |
| MAILDIR=DIRECTORY | Defines the directory to which mail is sent. If this directory does not already exist, be sure to create it. |