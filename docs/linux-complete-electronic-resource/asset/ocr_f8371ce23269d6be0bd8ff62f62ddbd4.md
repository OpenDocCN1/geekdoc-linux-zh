# SEE ALSO

lpr(1), lpq(1), lpd(8)

# DIAGNOSTICS

*"Permission denied"* if the user tries to remove files other than his own.

# BUGS

Since there are race conditions possible in the update of the lock file, the currently active job may be incorrectly identified.

# HISTORY

The **lprm** command appeared in 3.0BSD.

# LS(1)

# NAME

**ls, dir, vdir**  List contents of directories.

# SYNOPSIS

ls [-abcdgiklmnnpqrstuxABCDFGLNQRSUX1] [-w cols] [-T cols]
[-l pattern] [-all] [-escape] [-directory] [-node] [-kilobytes]
[-numeric-uid-gid] [-no-group] [-hidecontrol-chars]
[-reverse] [-size] [-width=cols] [-tabsize=cols] [-almost-all]
[-ignore-backups] [-classify] [-file-type] [-full-time]
[-ignore=pattern] [-dereference] [-literal] [-quote-name]
[-recursive] [-sort= { none,time,size,extension }]
[ -format={ long,verbose,commas,across,vertical,single-column}]
[ -time={ time,access,use,ctime,status }]
[ -help] [ -version]
[-color[= { yes,no, tty}]] [-colour= { yes,no, tty}]] [name...] 

# DESCRIPTION

This documentation is no longer being maintained and may be inaccu-rate or incomplete. The Texinfo documentation is now the authoritative source.