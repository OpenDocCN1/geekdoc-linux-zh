# Table 17.1 logrotate Configuration File Directives

| Directive | Action |
| :--- | :--- |
| **compress** | Uses **gzip** to compress the old log file. See also **nocompress**. |
| **copytruncate** | Copies the active log to create the backup, then truncates the active log file. Use this directive when you have processes appending to open files. **copytruncate** allows the log process to continue writing to the open file. |
| **create** _mode_ _owner_ _group_ | Rotates out the old file, and creates the new file with **(optional)** specified _mode_, _owner_, and _group_. If omitted, the _mode_, _owner_, and _group_ of the new file will be those of the old file. The **create** is done before the **postrotate** script, if one is present. See also **nocreate**. |
| **daily** | Rotates logs every day. |
| **delaycompress** | If used in conjunction with **compress**, doesn't compress the file rotated out until the next time this file is cycled. |
| **errors** _address_ | Mails any logrotate errors to _address_. |
| **ifempty** | Rotates the log file even if it is empty. This is the default behavior; also see **notifempty**. |
| **include** _file|directory_ | Reads _file_ or files in _directory_, ignoring nonregular files and files ending with a taboo extension (see **tabooext**). Files are processed as if they appeared inline in the file that included them. |
| **mail** _address_ | Mails files being cycled out of existence to _address_. See also **nomail**. |
| **monthly** | Cycles log files monthly. They are cycled the first time **logrotate** runs each month, normally the first day of the month. |
| **nocompress** | Does not compress cycled log files. See also **compress**. |
| **nocopytruncate** | Creates a copy of the original log, but does not truncate the original file. See also **copytruncate**. |
| **nocreate** | Overrides the **create** option; no new log files will be created. |
| **nodelaycompress** | Overrides **delaycompress**. Compression is done at cycle time. |
| **nomail** | When log files are cycled out of existence, does not mail a copy. See also **mail** _address_. |
| **noolddir** | Keeps cycled logs in the same directory as the current log(s). See also **olddir** _directory_. |
| **notifempty** | Does not rotate the log if it is empty. See also **ifempty**. |
| **olddir** _directory_ | Keeps cycled logs in _directory_. _directory_ must be on the same file system as the current log(s). |