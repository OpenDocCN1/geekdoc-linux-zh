git reflog expire removes reflog entries older than this time and are not reachable from the current tip; defaults to 30 days. With “<pattern>” (e.g. “refs/stash”) in the middle, the setting applies only to the refs that match the <pattern>.

# gc.rerereResolved

Records of conflicted merge you resolved earlier are kept for this many days when git rerere gc is run. The default is 60 days. See (1).

# gc.rerereUnresolved

Records of conflicted merge you have not resolved are kept for this many days when git rerere gc is run. The default is 15 days. See (1).

# gitcvs.commitMsgAnnotation

Append this string to each commit message. Set to empty string to disable this feature. Defaults to “via git-CVS emulator”.

# gitcvs.enabled

Whether the CVS server interface is enabled for this repository. See (1).

# gitcvs.logFile

Path to a log file where the CVS server interface well… logs various stuff. See (1).

# gitcvs.usercrfileattr

If true, the server will look up the end-of-line conversion attributes for files to determine the -k modes to use. If the attributes force Git to treat a file as text, the -k mode will be left blank so CVS clients will treat it as text. If they suppress text conversion, the file will be set with -kb mode, which suppresses any newline munging the client might otherwise do. If the attributes do not allow the file type to be determined, then gitcvs.allBinary is used. See (5).

# gitcvs.allBinary

This is used if gitcvs.usercrfileattr does not resolve the correct -kb mode to use. If true, all unresolved files are sent to the client in mode -kb. This causes the client to treat them as binary files, which suppresses any newline munging it otherwise might do. Alternatively, if it is set to “guess”, then the contents of the file are examined to decide if it is binary, similar to core.autocrlf.

# gitcvs.dbName

Database used by git-cvsserver to cache revision information derived from the Git repository. The exact meaning depends on the used database driver, for SQLite (which is the default driver) this is a filename. Supports variable substitution (see (1) for details). May not contain semicolons (;). Default: %Ggitcvs.%m.sqlite

# gitcvs.dbDriver

Used Perl DBI driver. You can specify any available driver for this here, but it might not work. git-cvsserver is tested with DBD::SQLite, reported to work with DBD::Pg,