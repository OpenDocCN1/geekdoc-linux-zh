# CONTROL STRUCTURES 983

links to the script or rename it, the usage and error messages will still provide accurate information.

Another feature of safefit relates to the use of the $$ parameter in the name of a temporary file. The statement following the esac statement creates and assigns a value to the tempfile variable. This variable contains the name of a temporary file that is stored in the /tmp directory, as are many temporary files. The begins with the PID number of the shell and ends with the name of the script. Using the PID number ensures that the filename is unique. Safedit will not attempt to overwrite an existing file, if the script is appended to that, so that the file is left in /tmp for some reason, you can figure out where it came from.

The PID number is written in front of—rather after—Script in the filename because of the 14-character limit placed on filenames by older versions of UNIX. Linux systems do not have this limitation. Because the PID number ensures the uniqueness of the filename, it is placed so it cannot be truncated. (If the Script is truncated, the filename is still unique.) For that reason, when a backup file is created inside the control structure a few lines down the script, the filename consists of the string bak, followed by the name of the file being edited. On an older system, if bak used as a suffix rather than a prefix and the original filename were 14 characters long, bak might be lost and the original file be overwritten. The basename utility extracts the simple filename of Editfile before it is prefixed with bak.

The safedit script uses an unusual test-command in the if structure: vim.tiny Editfile. The test-command calls vim to edit Editfile. When you finishing the file and exit from vim, vim returns an exit code. If the control structure uses that exit code to determine which branch to take. If the editing session completes successfully, vim returns 0 and the statements following the then statement are executed. If vim does not terminate normally (as would occur if the user killed [page 455] the vim process), vim returns a nonzero exit status and the script executes the statements following else.

# select

The select control structure is based on the one found in the Korn Shell. It displays a menu, assigns a value to a variable based on the user's choice of items, and executes a series of commands. The select control structure has the following syntax:

```
select varname [in arg ...]
do
  commands
done
```

The select structure displays a menu of the arg items. If you omit the keyword in and the list of arguments, select uses the positional parameters in place of the arg