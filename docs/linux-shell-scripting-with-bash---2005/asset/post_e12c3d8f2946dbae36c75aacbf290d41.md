
interactive shell is not necessarily a login shell. A user can start a non-login interactive shell by typing `bash` at a Bash prompt, thus starting a new copy of Bash.

Whether the Bash session is interactive or a login shell determines which profile files are used. This way, Bash separates commands specifically for customizing an interactive session from the more general-purpose commands.

The `/etc/profile` file contains the setup commands and environment changes common to all users. A general profile file might look something like this:

```bash
#!/etc/profile
# No core files by default
ulimit -S -C 0 > /dev/null 2>&1
# HOSTNAME is the result of running the hostname command
declare -x HOSTNAME="`/bin/hostname`"
# No more than 1000 lines of Bash command history
declare -x HISTSIZE=1000
# If PostgreSQL is installed, add the Postgres commands
# to the user's PATH
if test -r /usr/bin/psql/bin ; then
    declare -x PATH="${PATH}*:*/usr/bin/psql/bin"
fi
# end of general profile
```

Only the superuser can edit this file. When Bash is used as a login shell, it executes the first file it finds named `~/.bash_profile`, `~/.bash_login`, or `~/.profile`. When a session completes, Bash runs `~/.bash_logout`, if it exists.

For example, SuSE Linux uses `~/.profile` for the user's profile file. (You can check this by listing the files in your home directory.) By editing this file, you can add commands that will always execute when you log in.

```bash
# My profile
short -S -O emacs     # I prefer emacs mode to vi mode
date                  # display the date when I log on
```

Test the changes by simulating a login with the `--login` switch.

```bash
$ bash --login
Wed Feb 6 15:20:35 EST 2002
$ short -O emacs
emacs                 on
$ logout
```

Running a new Bash interactive session without logging in will not run the profile file.

```bash
$ bash
$ logout
bash: logout: not login shell: use 'exit'
$ exit
```

Scripts will not normally execute the login profile scripts. Bash will load a profile for scripts if the `BASH_ENV` environment variable contains a pathname to a file to execute. However, you should avoid using `BASH_ENV`. Setting the common environment for a set of scripts is usually done with the `source` command, which is discussed in Chapter 14, “Functions and Script Execution.” `BASH_ENV` has no effect on interactive sessions.

You can stop the running of the login profile files by using the `--noprofile` switch.

Bash runs a different set of files for interactive sessions that are not also login sessions. Bash looks for a customization script called `~/.bashrc` (Bash resources) and executes it instead of the login profile files. Aliased functions are only allowed in the resource files. A different resource file can be specified with the `--init-file` or `--rcfile` switch. A typical resource file might contain the following:

```bash
# /etc/bashrc
# Don't let others write to the user's files
umask 002
# Alias ls to provide default switches
alias ls='ls -qF'
```

Some distributions add lines to your login profile to run the commands in `~/.bashrc` as well. This is not a feature of Bash, but a change made by your Linux distribution. You can add the following lines to the `~/.bashrc` file to test its behavior:

```bash
# My bashrc Resource File Customizations
printf "\n" ".bashrc has run"
```

Test it from the command prompt by starting new sessions. In this case, SuSE Linux always runs the resource file.

```bash
$ bash --login
.bashrc has run
$ logout
$ bash
.bashrc has run
$ exit
```

As a result, you cannot be certain of the behavior of the resource file without checking your distribution.

Resource files can be suppressed with the `--norc` switch. Your distribution can run other files as well during login:

- Red Hat and Mandrake Linux separates your customizations, putting functions and aliases in `~/.bashrc` and other customization in `~/.bash_profile`. Their `.bash_profile` script will automatically run a `.bashrc` file as well, if it is present.
- SuSE Linux separates your customizations, putting functions and aliases in `~/.bashrc` and other customization in `~/.profile`. Their `.profile` script will automatically run a `.bashrc` file as well, if it is present.
- SCO Linux (also called Caldera Linux) uses `~/.profile`, which calls `~/.bashrc`. It then runs the profile script from `/etc/config.d/shells` to configure the system defaults. When `~/.bashrc` runs, it calls `/etc/config.d/shells/bashrc` to set up the non-interactive defaults. User's personal customizations should be stored in `~/.profile.private` and `~/.bashrc.private`, respectively.

Likewise, the general profile files can be customized:

- Red Hat and Mandrake split customizations into `/etc/bashrc` and `/etc/profile` to mimic the behavior of a user's profile files. Further system scripts automatically executed are for specifically installed packages stored in `/etc/profile.d`.
- SuSE Linux automatically set the contents of many files in the `/etc` directory, including `/etc/profile`. As a result, personal changes must stored in a separate file called `/etc/profile.local` or they can be lost when the system is reconfigured or upgraded. Other system scripts automatically executed are `/etc/SuSEconfig` and scripts for installed software packages stored in `/etc/profile.d`. SuSE also includes an `/etc/profile.dos` script to define customizations for users coming from MS-DOS. This is enabled by SuSE configuration software, but it can also be executed from your `/etc/profile.local` file.
- SCO Linux only puts minimum setup information common to any Bourne-based shells in `/etc/profile`. Common Bash settings should be configured in `/etc/config.d/shells/profile` and `/etc/config.d/shells/bashrc`.

## Reference Section

### ls Command Switches

- `--all` (or `-a`)—Shows all files, including `.` and `..`
- `--almost-all` (or `-A`)—Shows all files except `.`, and `..`
- `--block-size=n`—Shows the size of files as n-byte blocks
- `--classify` (or `-F`)—Appends a symbol to a filename to indicate its type
- `--color=t`—Uses color for filenames, t equals never, always, or auto.
- `--dereference` (or `-L`)—Shows items referenced by symbolic links
- `--directory` (or `-d`)—Shows information about a directory instead of showing its contents
- `--dired` (or -D)—Output for emacs `dired` mode
- `--escape` (or `-b`)—Prints octal escape sequences for unprintable characters
- `--file-type` (or -p)—Same as `--classify`
- `--format=across` (or -x)—Sorts by lines instead of columns
- `--format=commas` (or -m)—Shows filenames as a list separated by commas
- `--format=long` (or -1)—Shows detailed (long) listings
- `--format=single-column` (or `-1`)—Shows results as one file per line
- `--format=verbose`—Same as the long format
- `--format=vertical` (or `-c`)—Lists entries by columns
- `--full-time`—Shows full date and time
- `--hide-control-chars` (or `-q`)—Displays a ? for unprintable characters in file-names
- `--human-readable` (or `-h`)—Shows sizes in kilobytes, megabytes, and so on, instead of raw bytes
- `--ignore=p` (or `-I`)—Ignores files matching the pattern `p`
- `--ignore-backups` (or `-B`)—Does not list files ending with `~`
- `--indicator-style=classify`—Same as `--classify`
- `--indicator-style=none`—Don’t classify files
- `--indicator-style=file-type`—Same as `--file-type`
- `--inode` (or `-i`)—Prints the inode number for the file
- `--kilobytes` (or `-k`)—Same as block size 1024
- `-f`—Does not sort, enable `-a`, disable `-1`
- `--literal` (or `-8`)—Shows unprintable characters in names as-is (unlike `-q`)
- `--no-group` (or `-g`)—Hides the group that owns the file
- `--numeric-uid-gid` (or `-n`)—Shows UIDs and GIDs as numbers not names
- `-o`—Shows long listings without the file group ownership information
- `--quote-name` (or `-Q`)—Encloses filenames in double quotes
- `--quoting-style=literal`—Same as `--literal`
- `--quoting-style=locale`—Uses locale’s quoting style around individual file-names
- `--quoting-style=shell`—Uses shell quoting when necessary around individual filenames
- `--quoting-style=shell-always`—Always uses shell quoting around individual filenames
- `--quoting-style=c`—Uses C string quoting around individual filenames
- `--quoting-style=escape`—Escapes special characters with backslashes
- `--reverse` (or `-r`)—Reverses the sorting order
- `--recursive` (or `-R`)—Lists the contents of all subdirectories
- `-si` (or `-h`)—Similar to `--human-readable`, but uses powers of 1000 instead of 1024
- `--size` (or `-s`)—Prints the size in blocks
- `--sort=size` (or `-S`)—Sorts by file size
