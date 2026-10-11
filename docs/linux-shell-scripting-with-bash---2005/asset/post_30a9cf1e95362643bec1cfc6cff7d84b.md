
replaced. Any suffix provided by the `-s` switch or prefix provided by the `-P` switch are added to all surviving items. This is the final list.

```bash
$ compgen -A directory -X tia t
test
texttools
$ compgen -A directory -S '.txt,' -X tia t
test.txt
texttools.txt
```

The `complete` command sets the default completion behavior when completing a certain command. It uses the same options as `compgen`, but saves them for future use with the command. You can also assign completion commands and functions this way.

```bash
$ compgen -A directory t
temp
tia
texttools
$ complete -A directory -X tia ls
$ ls t
temp
texttools
$ complete -A directory -P info ls
$ ls t
Cmd=ls P=info ls
$ complete -p ls
complete -d -P info ls
```

The `-p` (`print`) switch lists the currently defined completion for a command.

```bash
$ complete -r ls
$ complete -d -P info ls
```

The `-r` (`remove`) command removes the defined completion.

The `-o` (`option`) switch sets various options. `-o dirnames` attempts to match directories if no other matches exist. `-o filenames` allows the word to be altered (such as dropping a trailing slash) to help identify matches. `-o default` is the default, providing no special handling when a match fails. Newer versions of Bash also support `-o nospace`, which prevents a space from being appended to the end of a completed word.

The completion commands can be combined with functions to create powerful new command-line utilities.

## Locales

Under Linux, the language and culture of a user is represented by his or her “locale.” The locale information is stored in environment variables. Some of the standard ones are:

- `LC_CTYPE`—The character classes and case conversion
- `LC_COLLATE`—The collating sequence for the character set
- `LC_NUMERIC`—The radix character (character used to separate number from base) and thousands separator
- `LC_MONETARY`—Like `LC_NUMERIC`, but for formatting money
- `LC_MESSAGES`—The formatting of diagnostic messages and user dialogue
- `LC_TIME`—The local month spellings and other aspects of date formatting

Each of these variables contains a locale category name to use. The categories are stored in a locale database located in `/usr/lib/locale`. The database is updated with the Linux `localedef` command.

The `locale` command displays the current locale settings. `en_US` is the category for United States English, `en_CA` is Canadian English, `fr_CA` is Canadian French, and so forth.

```bash
$ locale
LANG=en_US
LC_CTYPE="en_US"
LC_NUMERIC="en_US"
LC_TIME="en_US"
LC_COLLATE="en_US"
LC_MONETARY="en_US"
LC_MESSAGES="en_US"
LC_PAPER="en_US"
LC_NAME="en_US"
LC_ADDRESS="en_US"
LC_TELEPHONE="en_US"
LC_MEASUREMENT="en_US"
LC_IDENTIFICATION="en_US"
LC_ALL=
```

`locale -a` (`all`) displays a list of all locale categories. The `-m` (`map`) switch displays a list of all character mappings.

Locales are usually selected by the user during the Linux installation process. To change the locale, assign new values to an `LC` variable.

```bash
$ LC_NUMERIC=fr_CA # use French Canadian number conventions
```

Certain Bash and Linux commands are affected by the settings. For example, dollar double quote substitution converts a string to the preferred character set for the current locale. The value of `LC_COLLATE` affects the order in which pathname are pattern matched by Bash as well as the sorting order of the Linux `sort` command.

## The du Command

The Linux `du` (`disk usage`) command shows the amount of disk space used by a directory and all subdirectories within it. The `-s` (`summarize`) switch displays only the grand total. The `--human-readable` (or `-h`) switch converts the total to the nearest megabytes or gigabytes.

```bash
$ pwd
/home/kburch
$ du --summarize --human-readable
36M		.
$ du --summarize --human-readable . archive
36M		.
28M		archive
```

For scripts, there are a number of switches controlling how the results are grouped and what units are used. The space totals can be in bytes (or `-b`), kilobytes (or `-k`), megabytes (or `-m`), or blocks of `-blocksize=b` bytes. The default units are kilobytes. The `-si` (or `-h`) switch uses units of 1000 instead of 1024. You can determine a `-total` (or `-c`) for all files on the command line, as well as totals for `-all` (or `-a`) all files within directories. `-separate-dirs` (or `-s`) shows the totals for subdirectories, the default behavior.

The amounts and the filenames are separated by a Tab character. To extract one column or the other, use the `cut` command.

```bash
$ TAB=$(printf '\t')
$ du -all -kilobytes incoming_orders | cut -d"$TAB" -f1
20
12
40
56
132
```

Other switches affect the way files are searched. The `-dereference-args` (or `-D`) switch dereferences paths that are symbolic links. The `-count-links` (`-l`) switch counts each hard link to the same file as separate files. The `-one-file-system` (`-x`) switch constrains the search to the current file system. The search can be constrained to `-max-depth=n` levels of subdirectories, or can exclude any files with `-exclude=pattern` or a list of files in a file with `-exclude-from=file` (or `-X file`).

## Memory Usage

The Linux `free` command reports the memory usage on the system.

```bash
$ free
              total        used        free      shared  buffers  cached
Mem:         61792       58756        3036       10116    36152    8988
-/+ buffers/cache:      13616       48176
Swap:        514072        8180      505892
```

The total, used, and free columns are the total amount of memory, the amount of memory currently used by the Linux kernel, and the amount of free memory, respectively. The free and used columns always add up to the total. The last three columns show how the used memory is allocated; within shared memory, buffers, or caches. The final line shows the swap space allocated, used, and free on disk.

The `-t` switch displays an additional total line.

```bash
$ free -t
              total        used        free      shared  buffers  cached
Mem:         61792       58760        3032       10136    36152    8988
-/+ buffers/cache:      13620       48172
Swap:        514072        8180      505892
Total:       575864       66940      508924
```

By default, the display is in kilobytes. The `-b` switch displays bytes, and the `-m` switch displays megabytes.

`free` is not script-friendly. To get the information you need, you have to use `cut` and `grep`. The columns are separated by spaces, which must be compressed for use with `cut`.

```bash
$ free | grep "Mem"
Mem: 61792 58880 2912 10120 36156 9068
$ free | grep "Mem" | tr -s ' '
Mem: 61792 58876 2916 10120 36156 9068
$ free | grep "Mem" | tr -s ' ' | cut -d' ' -f2
61792
```

## noclobber and Forced Overwriting

Normally, when standard output is redirected using `>`, an existing file with the same name is overwritten.

```bash
$ printf "First line\n" > temp.txt
$ printf "Second line\n" > temp.txt
$ cat temp.txt
Second line
```

To provide a safety measure against overwriting an important file, the `noclobber` shell option prevents a file from being overwritten by a redirection.

```bash
$ shopt -s noclobber
$ printf "First line\n" > temp.txt
$ printf "Second line\n" > temp.txt
bash: temp.txt: cannot overwrite existing file
```

A file can be forcibly overwritten using `>|` instead of `>`.

```bash
$ printf "Second line\n" >| temp.txt
$ cat temp.txt
Second line
```

The `noclobber` option is primarily intended for interactive sessions whereby a user might type the wrong filename. However, it can also be used as a debugging tool in scripts, identifying places where `>` is used instead of `>` or where files are not cleaned up between script runs.

For example, in the following script fragment, a log is created, but the date is missing from the log. Using `noclobber`, Bash displays an error for the line overwriting the date.

```bash
#!/bin/bash

shopt -s noclobber

declare -rx LOG="log.txt"

date > $LOG
printf "Results of night batch run:\n" > $LOG

# etc.
```

The `printf` should use `>>` redirection. `>` shouldn't be used in a script because it defeats the purpose of using `noclobber`.

## The fc Command

The built-in `fc` (*fix command*) command lists and edits the command history. This command has been largely superseded by the `history` and `!` history recall commands.

`fc` starts the default editor to alter the last command executed. When you leave the editor, the command executes. Instead of the entire command, only the first characters of a command are needed to make a match. Alternatively, you can specify a range of lines to edit. If the lines begin with a minus sign, the lines are counted from the end of the history (with `-1` being the most recent command).

With the `-s` (*substitute*) switch, instead of starting the editor, `fc` substitutes all occurrences of a word that you specify before executing the command for another word. For example, to edit a file with `pico` and then compile the file with the `gcc` compiler, use `-s "pico=gcc"` to substitute `gcc` for `pico`.

```bash
$ pico project.c
$ fc -s "pico=gcc" p
gcc project.c
```

The `-l` (*list*) switch lists the most recent items in the history, and you can specify the first line, or the first and last lines, to display. The `-n` (*no line numbers*) switch suppresses the line numbers in the history, and `-r` (*reverse*) reverses the order in which they are printed.

## ! Word Designators and Modifiers

The basic features of the `!` history recall command were discussed in Chapter 3. In fact, `!` has a number of features that enable you to select which command is recalled and determine whether or not new information should be substituted into the command before executing it.
