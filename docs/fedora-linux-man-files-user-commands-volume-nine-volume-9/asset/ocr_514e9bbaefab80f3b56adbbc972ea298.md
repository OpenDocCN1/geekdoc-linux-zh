# OPTIONS

The following options are understood:

+   - **`--icon=`**
+     Specify an icon alongside the password query, which may be used in all agents supporting graphical display. The icon should follow the **XDG Icon Naming Specification**\[\].

+   - **`--tiout=`**
+     Specify the query tiout in seconds. Defaults to 90s. A tiout of 0 waits indefinitely.

+   - **`--echo`**
+     Echo the user input instead of masking it. This is useful when using systemd-ask-password to query for usernas.

+   - **`--no-tty`**
+     Never ask for password on current TTY even if one is available. Always use agent system.

+   - **`--accept-cached`**
+     If passed, accept cached passwords, i.e. passwords previously typed in.

+   - **`--multiple`**
+     When used in conjunction with **`--accept-cached`** accept multiple passwords. This will output one password per line.

+   - **`-h`, **`--help`**
+     Print a short help text and exit.