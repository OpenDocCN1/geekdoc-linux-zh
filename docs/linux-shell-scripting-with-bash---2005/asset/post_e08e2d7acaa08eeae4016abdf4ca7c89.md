
## Bash Options

### Table C.1 shopt Options

| Option | Default | Description |
| :------- | :------- | :------- |
| `-o allelexport` | Off | All variables that are modified or created are exported. |
| `-o braceexpand` | On | The shell performs curly brace expansion. |
| `cdable_vars` | Off | The built-in `cd` command assumes that unrecognized directories are variables containing a directory path. |
| `cdspell` | Off | Spell-checks the directory component in a `cd` path. |
| `checkhash` | Off | Verifies that commands in the command lookup table still exist before trying a path search for the command to run. |
| `checkwinsize` | Off | Determines whether the display window has been resized after every command. |
| `cmdhist` | On | Allows multiple line history command editing. |
| `dotglob` | Off | Allows `.files` in a pathname expansion. |
| `-o emacs` | Off | Use emacs-style line-editing keys. |
| `-o errexit` | Off | Exits immediately if a command exits with a non-zero status. |
| `execfail` | Off | Script fails when built-in `exec` command can’t execute a command. |
| `expand_aliases` | On | Allows aliases. |
| `extglob` | Off | Enables extended pattern-matching features for file-names. |
| `-o hashall` | On | Remembers the location of commands as they are looked up. |
| `histappend` | Off | Command history appends the history file instead of overwriting it. |
| `histredit` | Off | Enables user to edit failed history substitutions. |
| `-o histexpand` | On | Enables `!` style history substitution. |
| `-o history` | on | Enables command history. |
| `histverify` | Off | History substitutions can be further edited. |
| `hostcomplete` | On | Completes hostnames containing an `@`. |
| `huponexit` | Off | Sends a hang-up signal to all jobs still running when this script exits. |
| `-o ignoreeof` | Off | Ensures that an interactive shell will not exit upon reading end-of-file. |
| `interactive-comments` | On | Allows comments to appear in interactive commands. |
| `-o keyword` | Off | All assignment arguments are placed in the environment for a command, not just those that precede the command name. |
| `lithist` | Off | A line with multiple commands is split up and stored as separate commands in the command history. |
| `mailwarn` | Off | Informs the user when new mail arrives when at the shell prompt. |
| `-o monitor` | On | Enables job control. |
| `no_empty_cmd_completion` | Off | Doesn’t allow command completion on an empty line. |
| `nocaseglob` | Off | Ignores case when pattern-matching filenames. |
| `-o noclobber` | Off | If set, does not allow existing regular files to be overwritten by redirection of output. |
| `-o noexec` | Off | Reads commands but does not execute them. |
| `-o noglob` | Off | Disables filename generation (`*globbing*`). |
| `-o notify` | Off | Notifies users of job termination immediately. |
| `-o nounset` | Off | Treats unset variables as errors when substituting. |
| `nullglob` | Off | Patterns that do not match anything return an empty string instead of themselves. |
| `-o onecmd` | Off | Exits after reading and executing one command. |
| `-o physical` | Off | If set, does not follow symbolic links when executing commands, such as `cd`, that change the current directory. |
| `-o posix` | Off | Conforms to the POSIX 1003.2 standard. |
| `-o privileged` | Off | Turned on whenever the real and effective user IDs do not match. Disables processing of the `*`$ENV`* file and `-o` importing of shell functions. Turning this option off causes the effective uid and gid to be set to the real uid and gid. |
| `progcomp` | On | Enables programmable completion. |
| `shoptvars` | On | Process prompts strings for variables and parameters. |
| `restricted_shell` | - | On if the shell is a restricted shell. This option is read-only. |
| `shift_verbose` | Off | Returns an error when no parameters are left to shift. |
| `sourcepath` | On | Finds scripts for `.` or `source` commands using the `PATH` variable. |
| `-o verbose` | Off | Prints shell input lines as they are read. |
| `-o vi` | Off | Uses vi-style line-editing keys. |
| `xpg_echo` | Off | Built-in command `echo` processes escape sequences by default. |
| `-o xtrace` | Off | Prints commands and their arguments as they are executed. |

### Table C.2 Bash set Switches

| Switch | Description |
| :--- | :--- |
| `-a` | Same as `allexport` |
| `-b` | Same as `notify` |
| `-e` | Same as `errexit` |
| `-f` | Same as `noglob` |
| `-h` | Same as `hashall` |
| `-I` | Forces the shell to be an "interactive" one. Interactive shells always read `~/.bashrc` on startup |
| `-k` | Same as `keyword` |
| `-m` | Same as `monitor` |
| `-n` | Same as `noexec` |
| `-o option` | Changes a shopt option (same as `shopt -o`) |
| `-p` | Same as `privileged` |
| `-t` | Same as `oncmd` |
| `-u` | Same as `nounset` |
| `-v` | Same as `verbose` |
| `-x` | Same as `xtrace` |
| `-B` | Same as `braceexpand` |
| `-C` | Same as `noclobber` |
| `-H` | Same as `histexpand` |
| `-P` | Same as `physical` |

## Error Codes

The following list contains the C language short form for an error code, the error code numeric value, and a short description of the error.

| **C Name** | **Value** | **Description** |
| --- | --- | --- |
| `EPERM` | 1 | Operation not permitted |
| `ENOENT` | 2 | No such file or directory |
| `ESRCH` | 3 | No such process |
| `EINTR` | 4 | Interrupted system call |
| `EIO` | 5 | I/O error |
| `ENXIO` | 6 | No such device or address |
| `E2BIG` | 7 | Arg list too long |
| `ENOEXEC` | 8 | Exec format error |
| `EBADF` | 9 | Bad file number |
| `ECHILD` | 10 | No child processes |
| `EAGAIN` | 11 | Try again |
| `ENOMEM` | 12 | Out of memory |
| `EACCES` | 13 | Permission denied |
| `EFAULT` | 14 | Bad address |
| `ENOTBLK` | 15 | Block device required |
| `EBUSY` | 16 | Device or resource busy |
| `EEXIST` | 17 | File exists |
| `EXDEV` | 18 | Cross-device link |
| `ENODEV` | 19 | No such device |
| `ENOTDIR` | 20 | Not a directory |
| `EISDIR` | 21 | Is a directory |
| `EINVAL` | 22 | Invalid argument |
| `ENFILE` | 23 | File table overflow |
| `EMFILE` | 24 | Too many open files |
| `ENOTTY` | 25 | Not a tty device |
| `ETXTBSY` | 26 | Text file busy |
| `EFBIG` | 27 | File too large |
| `ENOSPC` | 28 | No space left on device |
| `ESPIPE` | 29 | Illegal seek |
| `EROFS` | 30 | Read-only file system |
| `EMLINK` | 31 | Too many links |
| `EPIPE` | 32 | Broken pipe |
| `EDOM` | 33 | Math argument out of domain |
| `ERANGE` | 34 | Math result not representable |
| `EDEADLK` | 35 | Resource deadlock would occur |
| `ENAMETOOLONG` | 36 | Filename too long |
| `ENOLCK` | 37 | No record locks available |
| `ENOSYS` | 38 | Function not implemented |
| `ENOTEMPTY` | 39 | Directory not empty |
| `ELOOP` | 40 | Too many symbolic links encountered |
| `EMOUNTDBLOCK` | - | Same as `EAGAIN` |
| `ENMSG` | 42 | No message of desired type |
| `EIDRM` | 43 | Identifier removed |
| `ECHRNG` | 44 | Channel number out of range |
| `EL2NSYNC` | 45 | Level 2 not synchronized |
| `EL3HLT` | 46 | Level 3 halted |
| `EL3RST` | 47 | Level 3 reset |
| `ELNRNG` | 48 | Link number out of range |
| `EUNATCH` | 49 | Protocol driver not attached |
| `ENOCSI` | 50 | No CSI structure available |
| `EL2HKT` | 51 | Level 2 halted |
| `EBADE` | 52 | Invalid exchange |
| `EBAAD` | 53 | Invalid request descriptor |
| `EXFULL` | 54 | Exchange full |
| `ENOANO` | 55 | No anode |
| `EBADRPC` | 56 | Invalid request code |
| `EBADSLT` | 57 | Invalid slot |
| `EDEADLOCK` | - | Same as `EDEADLK` |
| `EBFONT` | 59 | Bad font file format |
| `ENOSTR` | 60 | Device not a stream |
| `ENODATA` | 61 | No data available |
