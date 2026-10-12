+   1. Make a copy of the `/usr/sbin/logcheck` file. For example:
+      ```
+      # cp /usr/sbin/logcheck /usr/sbin/logcheck.old
+      ```

+   2. Open the script in any text editor while logged in as the `root` user and make any changes to the script. The following bullet list describes values that you may want to change in this script.

+   - **SYSADMIN**: This variable defines the `root` user as the one to receive the e-mail messages resulting from running Logcheck. You can change `root` to anyone you want to receive the Logcheck messages. This can be either local users or users on other computers (that is, `user@hostname`).
+      ```
+      SYSADMIN=root
+      ```

+   - **TMPDIR**: Sets where Logcheck writes its temporary files during processing. The directory is created when Logcheck starts and is removed before Logcheck finishes. You can change the location by modifying the following entry:
+      ```
+      TMPDIR=/tmp/logcheck$$_-$RANDOM
+      ```

+   - **GREP**: The logcheck script relies on a `grep` command that supports the `-i`, `-v`, and `-f` options to search the log files. By default, the `egrep` command is used for this purpose. You could change the value to `grep` or another command by modifying the following variable:
+      ```
+      GREP=egrep
+      ```

+   - **MAIL**: E-mail is sent by Logcheck using the `mail` command. To have Logcheck use a command other than the `mail` command to send e-mail messages to the administrator, change the following mail variable:
+      ```
+      MAIL=mail
+      ```

+   - **Filter files**: There are four filter files defined by Logcheck. The files each contain keywords that are either used to find messages or exclude messages that contain those keywords. The following variables are set to indicate the location of the four Logcheck filter files:
+      ```
+      HACKING_FILE=/etc/logcheck/logcheck.hacking
+      VIOLATIONS_FILE=/etc/logcheck/logcheck.violations
+      VIOLATIONS_IGNORE_FILE=/etc/logcheck/logcheck.violations.ignore
+      IGNORE_FILE=/etc/logcheck/logcheck.ignore
+      ```

For more information on filter files, see the "Changing Logcheck filter files" section, later in this chapter.

+   - **Log files**: The last entries in the `/usr/sbin/logcheck` script that you may want to change designate which log files are monitored by the logcheck script. By default, the logcheck script runs the `logtail` command to check the `messages`, `secure`, and `maillog` files (in `/var/log`). The following lines define which log files that are