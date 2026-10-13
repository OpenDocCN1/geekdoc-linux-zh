+   - `-M path`—Specify the list of directories to search for man pages. If no such option is given, the environment variable MANPATH is used. If no such environment variable is found, the default list is found by consulting `/etc/man.config`. An empty substring of MANPATH denotes the default list.
+   - `-P pager`—Specify which pager to use. This option overrides the MANPAGER environment variable, which in turn overrides the PAGER variable. By default, man uses `/usr/bin/less -is`.
+   - `-S section_list`—List is a colon-separated list of manual sections to search. This option overrides the MANSECT environment variable.
+   - `-a`—By default, man will exit after displaying the first manual page it finds. Using this option forces man to display all the manual pages that match name, not just the first.
+   - `-c`—Re-format the source man page, even when an up-to-date cat page exists. This can be meaningful if the cat page was formatted for a screen with a different number of columns, or if the preformatted page is corrupted.
+   - `-d`—Don’t actually display the man pages, but do print gobs of debugging information.
+   - `-D`—Don’t actually display the man pages, but do print gobs of debugging information. Both display and print debugging info.
+   - `-f`—Equivalent to whatis.
+   - `-F` or `--preformat`—Format only—do not display.
+   - `-h`—Print a one-line help message and exit.
+   - `-k`—Equivalent to apropos.
+   - `-K`—Search for the specified string in *all* man pages. Warning: This is probably very slow! It helps to specify a section. (Just to give a rough idea, on my machine this takes about a minute per 500 man pages.)
+   - `-m system`—Specify an alternate set of man pages to search based on the system name given.
+   - `-p string`—Specify the sequence of preprocessors to run before nroff or troff. Not all installations will have a full set of preprocessors. Some of the preprocessors and the letters used to designate them are: eqn, grap (g), pic (p), tbl (t), vgrind (v), refer (r). This option overrides the MANROFFSEQ environment variable.
+   - `-t`—Use `/usr/bin/groff -Tps -mandoc` to format the manual page, passing the output to stdout. The output from `/usr/bin/groff -Tps -mandoc` might need to be passed through some filter or another before being printed.
+   - `-w` or `--path`—Don’t actually display the man pages, but do print the location(s) of the files that would be formatted or displayed. If no argument is given, display (on stdout) the list of directories that is searched by man for man pages. If manpath is a link to man, manpath is equivalent to man -path.
+   - `-W`—Like -w, but print filenames one per line, without additional information. This is useful in shell commands like man -aw man | xargs ls -l.