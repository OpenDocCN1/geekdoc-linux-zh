The script defines the variables `$SYSNAME`, `$DESTDIR`, and `$TODAY`. `$SYSNAME` contains the name of the system and `$DESTDIR` the path of the directory to which the files should be copied. The latter should ideally point to a directory on another partition or, better yet, another hard disk. You should keep in mind that the files contain valuable information, enabling a possible intruder to compromise the system. They should be stored in a location only superusers have access to. `$TODAY` contains the current date, used as part of the name of the resulting tar archive. The archives won’t overwrite themselves this way, allowing you to create some kind of configuration history.

The choice of which `tar` program to use is Solaris specific. If the script is deployed on another *NIX system, you could use the path and name of the `tar` program installed there. If the system contains more than one `tar` program, customize the example function to make sure to create consistent archives.

The variables `$FILES` and `$DIRS` contain all files and directories to be backed up. They vary from system to system. If the Apache Web server is used, for example, you have to add the directory containing its configuration files to the `$DIRS` variable. The same goes for other configuration files important for the specific system.

The `copy_files()` function tests whether the respective file exists. If it exists, it copies the file and changes the filename in the following manner: `/etc/syslog.conf`, for example, becomes `unixhost_etc_syslog.conf` and so forth. This provides you with the means to identify the system the file was originally used on. Testing for the existence of a file allows you to deploy the script on similar systems without the need to customize it extensively. If the file does not exist, it won’t be copied, and there will be no error message. One requirement for this system to work as intended is no typos in the list of files. This shouldn’t be a problem because scripts should be tested thoroughly before deployment, anyway.

The `copy_directories()` function more or less mimics `copy_files()`, but does not add the name of the system to the directory. Saved directories in `$DESTDIR/$SYSNAME` start with an underscore, `_`.

The `make_tar` function creates the tar archive. It does not seem to be necessary to wrap the creation of the archive in a function, but doing so allows an easier extension of the script later.

The `dircheck()` function tests for the existence of the used directory structure in `$DESTDIR` and creates the directory should the test fail.

The real script starts after the comment `# main program`; all functions are executed in order of appearance. If the script is deployed by executing it via cron, writing an entry into a log file is a good idea. Most *NIX systems use the program logger for that purpose. It is used to send messages to the syslogd process. You could simply add the following line at the end of the script:

```
logger -p user.crit $0 done.
```