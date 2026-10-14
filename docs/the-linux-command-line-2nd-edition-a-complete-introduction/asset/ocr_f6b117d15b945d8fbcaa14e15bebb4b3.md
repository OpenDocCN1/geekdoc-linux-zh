programs and one that is well suited to shell programming in particular.

In this chapter, we will use top-down design to further develop our report-generator script.

# Shell Functions

Our script currently performs the following steps to generate the HTML document:

+   1. Open page.
+   2. Open page header.
+   3. Set page title.
+   4. Close page header.
+   5. Open page body.
+   6. Output page heading.
+   7. Output timestamp.
+   8. Close page body.
+   9. Close page.

For our next stage of development, we will add some tasks between steps 7 and 8. These will include:

+   - System uptime and load. This is the amount of time since the last shutdown or reboot and the average number of tasks currently running on the processor over several time intervals.
+   - Disk space. The overall use of space on the system’s storage devices.
+   - Home space. The amount of storage space being used by each user.

If we had a command for each of these tasks, we could add them to our script simply through command substitution:

```
#!/bin/bash

# Program to output a system information page

TITLE="System Information Report For $HOSTNAME"
CURRENT_TIME=$(date "+%x %r %Z")
TIMESTAMP="Generated $CURRENT_TIME, by $USER"

cat << _EOF_
<HTML>
    <HEAD>
```