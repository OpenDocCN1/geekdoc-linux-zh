# CAT PAGES

man will try to save the formatted man pages to save formatting time the next time these pages are needed. Traditionally, formatted versions of pages in `DIR/manX` are saved in `DIR/catX`, but other mappings from man dir to cat dir can be specified in `/etc/man.config`. No cat pages are saved when the required cat directory does not exist.

It is possible to make man suid to a user man. Then, if a cat directory has owner man and mode 0755 (only writable by man), and the cat files have owner man and mode 0644 or 0444 (only writable by man, or not writable at all), no ordinary user can change the cat pages or put other files in the cat directory. If man is not made suid, a cat directory should have mode 0777 if all users should be able to leave cat pages there.

The option -c forces reformatting a page, even if a recent cat page exists.

# ENVIRONMENT

+   - **MANPATH**—If `MANPATH` is set, its value is used as the path to search for manual pages.
+   - **MANROFFSEQ**—If `MANROFFSEQ` is set, its value is used to determine the set of preprocessors run before `nroff` or `troff`. By default, pages are passed through the table preprocessor before `nroff`.
+   - **MANSECT**—If `MANSECT` is set, its value is used to determine which manual sections to search.
+   - **MANWIDTH**—If `MANWIDTH` is set, its value is used as the width manpages should be displayed. Otherwise the pages can be displayed over the whole width of your screen.
+   - **MANPAGER**—If `MANPAGER` is set, its value is used as the name of the program to use to display the man page. If not, then pager is used. If that has no value either, `/usr/bin/less -is` is used.
+   - **LANG**—If `LANG` is set, its value defines the name of the subdirectory where man first looks for man pages. Thus, the command `LANG=dk man 1 foo` will cause man to look for the foo man page in `.../dk/man1/foo.1`, and if it cannot find such a file, then in `.../man1/foo.1`, where `...` is a directory on the search path.
+   - **NLSPATH, LC_MESSAGES, LANG**—The environment variables `NLSPATH` and `LC_MESSAGES` (or `LANG` when the latter does not exist) play a role in locating the message catalog. (But the English messages are compiled in, and for English no catalog is required.) Note that programs like `col(1)` called by man also use, for example, `LC_CTYPE`.
+   - **PATH**—`PATH` is used in the construction of the default search path for man pages.
+   - **SYSTEM**—`SYSTEM` is used to get the default alternate system name (for use with the `-m` option).

# SEE ALSO

`apropos(1), whatis(1), less(1), groff(1).`