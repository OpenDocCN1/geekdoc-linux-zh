
## FILES

/etc/rsyncd.conf or rsyncd.conf

## SEE ALSO

## BUGS

These are transferred as *nix mtimes.
When transferring to FAT filesystems, rsync may re-sync unmodified files. See the comments on the `--modify-window` option.
File permissions, devices, etc. are transferred as native numerical values.
See also the comments on the `--delete` option.
Please report bugs! See the web site at <http://rsync.samba.org/bugzilla/>

## VERSION

This man page is current for version 3.1.1 of rsync.

## INTERNAL OPTIONS

The options `--server` and `--sender` are used internally by rsync, and should never be typed by a user under normal circumstances. So awareness of these options may be needed in certain scenarios, such as when setting up a login that can only run an rsync command. For instance, the support directory of the rsync distribution has an example script `nadrrsync` (for restricted rsync) that can be used with a restricted ssh login.

## CREDITS

rsync is distributed under the GNU General Public License. See the file COPYING for details.

A WEB site is available at <http://rsync.samba.org/>. The site includes an FAQ-O-Matic which may cover questions unanswered by this manual page.

The primary ftp site for rsync is <ftp://rsync.samba.org/>.

We would be delighted to hear from you if you like this program. Please contact the mailing-list at <mailto:rsync-masters@lists.samba.org>.

This program uses the excellent zlib compression library written by Jean-loup Gailly and Mark Adler.

## THANKS

Special thanks go out to: John Van Essen, Matt McCutchen, Wesley W. Terpstra, David Dykstra, Jos Backus, Sebastian Krahr, Martin Pool, and our gone-but-not-forgotten comrade, J.W. Schultz.

Thanks also to Richard Brent, Brendan Mackay, Bill Waite, Stephen Rothwell and David Bell. I’ve probably missed some people, my apologies if I have.

## AUTHOR

rsync was originally written by Andrew Tridgell and Paul Mackerras. Many people have later contributed to it. It is currently maintained by Wayne Davison.

Mailing lists for support and development are available at <http://rsync.samba.org/mail.html>.

## RUNCON

### NAME

runcon - run command with specified SELinux security context

### SYNOPSIS

```
runcon CONTEXT COMMAND [args]
runcon [ -c ] [-u USER] [-r ROLE] [-t TYPE] [-l RANGE] COMMAND [args]
```

### DESCRIPTION

Run COMMAND with completely-specified CONTEXT, or with current or transitioned security context modified by one or more of LEVEL, ROLE, TYPE, and USER.

If none of *-c, -t, -u, -r, or -l* is specified, the first argument is used as the complete context. Any additional arguments after *COMMAND* are interpreted as arguments to the command.

Note that only carefully-chosen contexts are likely to successfully run.

Run a program in a different SELinux security context. With neither CONTEXT nor COMMAND, print the current security context.

Mandatory arguments to long options are mandatory for short options too.

-   **CONTEXT**
    Complete security context
-   **-c, --compute**
    Compute process transition context before modifying
-   **-t, --type=***TYPE*
    Type (for same role as parent)
-   **-u, --user=***USER*
    User identity
-   **-r, --role=***ROLE*
    Role
-   **-l, --range=***RANGE*
    Range
-   **--help**
    Display this help and exit
-   **--version**
    Output version information and exit

## AUTHOR

Written by Russell Coker.

## REPORTING BUGS

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
Report runcon translation bugs to <http://translationproject.org/team/>

## COPYRIGHT

Copyright 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>. This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

Full documentation at: <http://www.gnu.org/software/coreutils/runcon>
or available locally via: info `(coreutils) runcon invocation`

## VIM

### NAME

vim - Vi IMproved, a programmer's text editor

### SYNOPSIS

`vim` [options] [file ...]
`vim` [options] -
`vim` [options] -t tag
`vim` [options] -q [errorfile]
ex gex view gvim gview vimx evim eview rvim rview rgvim rgview

### DESCRIPTION

**Vim** is a text editor that is upwards compatible to Vi. It can be used to edit all kinds of plain text. It is especially useful for editing programs.

There are a lot of enhancements above Vi: multi-level undo, multiple windows and buffers, syntax highlighting, command line editing, filename completion, on-line help, visual selection, etc. See “help vi_diff.txt” for a summary of the differences between **Vim** and Vi.

While running **Vim** a lot of help can be obtained from the on-line help system, with the “:help” command. See the ON-LINE HELP section below.

Most often **Vim** is started to edit a single file with the command
`vim file`

More generally **Vim** is started with:
`vim [options] [filelist]`

If the filelist is missing, the editor will start with an empty buffer. Otherwise exactly one out of the following four may be used to choose one or more files to be edited.

-   **file ...**
    A list of filenames. The first one will be the current file and read into the buffer. The cursor will be positioned on the first line of the buffer. You can get to the other files with the “:next” command. To edit a file that starts with a dash, precede the filelist with “--”.
-   **-**
    The file to edit is read from stdin. Commands are read from stderr, which should be a TTY.
-   **-t {tag}**
    The file to edit and the initial cursor position depends on a “tag”, a sort of goto label. {tag} is looked up in the tags file, the associated file becomes the current file and the associated command is executed. Mostly this is used for C programs, in which case {tag} could be a function name. The effect is that the file containing that function becomes the current file and the cursor is positioned on the start of the function. See “:help tag-commands”.
-   **-q [errorfile]**
    Start in quickFix mode. The file [errorfile] is read and the first error is displayed. If [errorfile] is omitted, the filename is obtained from the ‘errorfile’ option (defaults to “AztecC.Err” for the Amiga, “errors.err” on other systems). Further errors can be jumped to with the “:cn” command. See “:help quickfix”.

**Vim** behaves differently, depending on the name of the command (the executable may still be the same file).

`vim`
The “normal” way, everything is default.

`ex`
Start in Ex mode. Go to Normal mode with the “:vi” command. Can also be done with the “-e” argument.

`view`
Start in read-only mode. You will be protected from writing the files. Can also be done with the “-R” argument.

`gvim` `gview`
The GUI version. Starts a new window.

`gex`
Starts a new gvim window in Ex mode. Can also be done with the “-e” argument to gvim.

`vimx`
Starts gvim in “Vi” mode similar to “vim”, but with additional features like xterm clipboard support.

`evim` `eview`
The GUI version in easy mode. Starts a new window. Can also be done with the “-y” argument.

`rvim` `rview` `rgvim` `rgview`
Like the above, but with restrictions. It will not be possible to start shell commands, or suspend **Vim**. Can also be done with the “-Z” argument.

### OPTIONS

The options may be given in any order, before or after filenames. Options without an argument can be combined after a single dash.

-   **+[num]**
    For the first file the cursor will be positioned on line “num”. If “num” is missing, the cursor will be positioned on the last line.
-   **+/ {pat}**
    For the first file the cursor will be positioned on the first occurrence of {pat}. See “help search-pattern” for the available search patterns.
-   **+{command}**
    -   **-c {command}**
        {command} will be executed after the first file has been read. {command} is interpreted as an Ex command. If the {command} contains spaces it must be enclosed in double quotes (this depends on the shell that is used). Example: Vim “+set si” main.c
        Note: You can use up to 10 “+” or “-c” commands.
-   **-S {file}**
    {file} will be sourced after the first file has been read. This is equivalent to -c “source {file}”. {file} cannot start with ‘-’. If {file} is omitted “Session.vim” is used (only works when -S is the last argument).
-   **--cmd {command}**
    Like using “-c”, but the command is executed just before processing any vimrc file. You can use up to 10 of these commands, independently from “-c” commands.
-   **-A**
    If **Vim** has been compiled with ARABIC support for editing right-to-left oriented files and Arabic keyboard mapping, this option starts **Vim** in Arabic mode, i.e. ‘arabic’ is set. Otherwise an error message is given and **Vim** aborts.
-   **-b**
    Binary mode. A few options will be set that makes it possible to edit a binary or executable file.
-   **-C**
    Compatible. Set the ‘compatible’ option. This will make **Vim** behave mostly like Vi, even though a .vimrc file exists.
-   **-d**
    Start in diff mode. There should be two, three or four filename arguments. **Vim** will open all the files and show differences between them. Works like `diff(1)`.
-   **-d {device}**
    Open {device} for use as a terminal. Only on the Amiga. Example: “-d con:20/30/600/150”.
-   **-D**
    Debugging. Go to debugging mode when executing the first command from a script.
-   **-e**
    Start **Vim** in Ex mode, just like the executable was called “ex”.
