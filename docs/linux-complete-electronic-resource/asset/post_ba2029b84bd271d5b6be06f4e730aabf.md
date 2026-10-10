
## man

- **-M path**  
  Specify the list of directories to search for man pages. If no such option is given, the environment variable `MANPATH` is used. If no such environment variable is found, the default list is found by consulting `/etc/man.config`. An empty substring of `MANPATH` denotes the default list.

- **-P pager**  
  Specify which pager to use. This option overrides the `MANPAGER` environment variable, which in turn overrides the `PAGER` variable. By default, `man` uses `/usr/bin/less`.

- **-S section_list**  
  List is a colon-separated list of manual sections to search. This option overrides the `MANSECT` environment variable.

- **-a**  
  By default, **man** will exit after displaying the first manual page it finds. Using this option forces **man** to display all the manual pages that match *name*, not just the first.

- **-c**  
  Reformat the source man page, even when an up-to-date cat page exists. This can be meaningful if the cat page was formatted for a screen with a different number of columns.

- **-d**  
  Don’t actually display the man pages, but do print gobs of debugging information.

- **-D**  
  Both display and print debugging info.

- **-f**  
  Equivalent to `whatis`.

- **-h**  
  Print a one-line help message and exit.

- **-k**  
  Equivalent to `apropos`.

- **-K**  
  Search for the specified string in *all* man pages. Warning: this is probably very slow! It helps to specify a section. (Just to give a rough idea, on my machine this takes about a minute per 500 man pages.)

- **-m system**  
  Specify an alternate set of man pages to search based on the system name given.

- **-p string**  
  Specify the sequence of preprocessors to run before *nroff* or *troff*. Not all installations will have a full set of preprocessors. Some of the preprocessors and the letters used to designate them are: `eqn` (e), `grap` (g), `pic` (p), `tbl` (t), `vgrind` (v), `refer` (r). This option overrides the `MANROFFSEQ` environment variable.

- **-t**  
  Use `/usr/bin/groff -Tps -mandoc` to format the manual page, passing the output to stdout. The output from `/usr/bin/groff -Tps -mandoc` may need to be passed through some filter or another before being printed.

- **-w or --path**  
  Don’t actually display the man pages, but do print the location(s) of the files that would be formatted or displayed. If no argument is given: display (on stdout) the list of directories that is searched by **man** for man pages. If **manpath** is a link to man, then `manpath` is equivalent to `man --path`.

- **-W**  
  Like -w, but print file names one per line, without additional information. This is useful in shell commands like `man -aW man | xargs ls -l`

### CAT PAGES

Man will try to save the formatted man pages, in order to save formatting time the next time these pages are needed. Traditionally, formatted versions of pages in `DIR/manX` are saved in `DIR/catX`, but other mappings from man dir to cat dir can be specified in `/etc/man.config`. No cat pages are saved when the required cat directory does not exist.

It is possible to make man suid to a user man. Then, if a cat directory has owner man and mode 0755 (only writable by man), and the cat files have owner man and mode 0644 or 0444 (only writable by man, or not writable at all), no ordinary user can change the cat pages or put other files in the cat directory. If **man** is not suid made, then a cat directory should have mode 0777 if all users should be able to leave cat pages there.

The option -c forces reformatting a page, even if a recent cat page exists.

### ENVIRONMENT

- **MANPATH**  
  If **MANPATH** is set, its value is used as the path to search for manual pages.

- **MANROFFSEQ**  
  If **MANROFFSEQ** is set, its value is used to determine the set of preprocessors run before running **nroff** or **troff**. By default, pages are passed through the table preprocessor before **nroff**.

- **MANSECT**  
  If **MANSECT** is set, its value is used to determine which manual sections to search.

- **MANWIDTH**  
  If *MANWIDTH* is set, its value is used as the width man pages should be displayed. Otherwise the pages may be displayed over the whole width of your screen.

- **MANPAGER**  
  If *MANPAGER* is set, its value is used as the name of the program to use to display the *man* page. If not, then *PAGER* is used. If that has no value either, `/usr/bin/less` is used.

- **LANG**  
  If *LANG* is set, its value defines the name of the subdirectory where man first looks for man pages. Thus, the command `LANG=dk man 1 foo` will cause man to look for a man page file in `.../dk/man1/foo.1`, and if it cannot find such a file, then in `.../man1/foo.1`, where `...` is a directory on the search path.

- **NLSPATH, LC_MESSAGES, LANG**  
  The environment variables *NLSPATH* and *LC_MESSAGES* (or *LANG* when the latter does not exist) play a role in locating the message catalog. (But the English messages are compiled in, and for English no catalog is required.) Note that programs like `col(1)` called by man also use e.g. `LC_CTYPE`.

- **PATH**  
  *PATH* is used in the construction of the default search path for man pages.

- **SYSTEM**  
  *SYSTEM* is used to get the default alternate system name (for use with the *-m* option).

### SEE ALSO

`apropos(1)`, `whatis(1)`, `less(1)`, `groff(1)`.

### BUGS

The *-t* option only works if a troff-like program is installed.

If you see blinking 55 or `<AD>` instead of hyphens, put `'LESSCHARSET=l latin1'` in your environment.

## MKDIR(1)

### NAME

**mkdir** Make directories.

### SYNOPSIS

```
mkdir [-p] [-m mode] [--parents] [--mode=mode] [-help] [--version] dir...
```

### DESCRIPTION

This documentation is no longer being maintained and may be inaccurate or incomplete. The Texinfo documentation is now the authoritative source. This manual page documents the GNU version of `mkdir`. **mkdir** creates a directory with each given name. By default, the mode of created directories is 0777 minus the bits set in the umask.

### OPTIONS

- **-m, --mode mode**  
  Set the mode of created directories to mode, which is symbolic as in `chmod` and uses the default mode as the point of departure.

- **-p, --parents**  
  Ensure that each given directory exists. Create any missing parent directories for each argument. Parent directories default to the umask modified by *u+wx*. Do not consider an argument directory that already exists to be an error.

- **-help**  
  Print a usage message on standard output and exit successfully.

- **-version**  
  Print version information on standard output then exit successfully.

## MORE(1)

### NAME

**more** File perusal filter for crt viewing.

### SYNOPSIS

```
more [-dlfpcsu] [-num] [+/ pattern] [+ linenum] [file ...]
```

### DESCRIPTION

**more** is a filter for paging through text one screenful at a time. This version is especially primitive. Users should realize that **less(1)** provides more(1) emulation and extensive enhancements.

### OPTIONS

Command line options are described below. Options are also taken from the environment variable **MORE** (make sure to precede them with a dash (-)) but command line options will override them.

- **-num**  
  This option specifies an integer which is the screen size (in lines).

- **-d**  
  **more** will prompt the user with the message "[Press space to continue, *q* to quit.]" and will display "[Press *h* for instructions.]" instead of ringing the bell when an illegal key is pressed.

- **-l**  
  **more** usually treats **^L** (form feed) as a special character, and will pause after any line that contains a form feed. The -l option will prevent this behavior.

- **-f**  
  Causes **more** to count logical, rather than screen lines (i.e., long lines are not folded).

- **-p**  
  Do not scroll. Instead, clear the whole screen and then display the text.

- **-c**  
  Do not scroll. Instead, paint each screen from the top, clearing the remainder of each line as it is displayed.

- **-s**  
  Squeeze multiple blank lines into one.

- **-u**  
  Suppress underlining.

- **+/ pattern**  
  The -+/ option specifies a string that will be searched for before each file is displayed.

- **+num**  
  Start at line number **num**.
