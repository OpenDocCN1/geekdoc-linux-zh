The /usr/local directory is similar in structure to the /usr directory. It has the following subdirectories, which are similar in purpose to those in the /usr directory:

+   /usr/local
+       - bin
+       - doc
+       - etc
+       - games
+       - info
+       - lib
+       - man
+       - sbin
+       +- src

# The /var Directory

Since the FHS requires that you be able to mount /usr read-only, any programs that write log files or need spool or lock directories probably should write them to the /var directory. The FHS states /var is for:

> "...variable data files. This includes spool directories and files, administrative and logging data, and transient and temporary files."

The following directories should be subdirectories of /var:

+   /var
+       - catman
+       - lib
+       - local
+       - lock
+       - log
+       - named
+       - nis
+       - preserve
+       - run
+       +-
+           - spool
+               - anacron
+               - at
+               - cron
+               - fax
+               - lpd
+               - mail
+               - mqueue
+               +-
+                   - news