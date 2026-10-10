files are being considered for remaking, which files are being compared and with what results, which files actually need to be remade, which implicit rules are considered and which are applied-everything interesting about how make decides what to do.

+   -e

Give variables taken from the environment precedence over variables from makefiles.

+   -f *file*

Use *file* as a makefile.

+   -i

Ignore all errors in commands executed to remake files.

+   -I *dir*

Specifies a directory *dir* to search for included makefiles. If several -I options are used to specify several directories, the directories are searched in the order specified. Unlike the arguments to other flags of *make*, directories given with -I flags may come directly after the flag: -I*dir* is allowed, as well as -I *dir*. This syntax is allowed for compatibility with the C preprocessor's -I flag.

+   -j *jobs*

Specifies the number of jobs (commands) to run simultaneously. If there is more than one -j option, the last one is effective. If the -j option is given without an argument, *make* will not limit the number of jobs that can run simultaneously.

+   -k

Continue as much as possible after an error. While the target that failed, and those that depend on it, cannot be remade, the other dependencies of these targets can be processed all the same.

+   -l -l *load*

Specifies that no new jobs (commands) should be started if there are others jobs running and the load average is at least *load* (a floating-point number). With no argument, removes a previous load limit.

+   -n

Print the commands that would be executed, but do not execute them.

+   -o *file*

Do not remake the file *file* even if it is older than its dependencies, and do not remake anything on account of changes in *file*. Essentially the file is treated as very old and its rules are ignored.