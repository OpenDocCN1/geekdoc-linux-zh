# Chapter Six: LINUX AND UNIXMAN COMMAND

On Linux and other Unix-like operating systems, *man* is the interface used to view the system's reference manuals.

# Syntax

```
```text
man [-C file] [-d] [-D] [-warnings[=warnings]] [-R encoding] [-L locale]
   [-m system[,...]] [-M path] [-S list] [-e extension] [-i|-I]
   [-regex|-wildcard] [-names-only] [-a] [-u] [no-subpages] [-P pager]
   [-r prompt] [-7] [-E encoding] [no-hyphenation] [no-justification]
   [-p string] [-t] [-T[device]] [-H[browser]] [-X[dpi]] [-Z]
   [[section] page ...] ...
man -k [apropos options] regexp ...
man -K [-w|-W] [-S list] [-i|-I] [-regex] [section] term ...
man -f [whatis options] page ...
man -l [-C file] [-d] [-D] [-warnings[=warnings]] [-R encoding]
   [-L locale] [-P pager] [-r prompt] [-7] [-E encoding] [-p string] [-t]
   [-T[device]] [-H[browser]] [-X[dpi]] [-Z] file ...
man -w|-W [-C file] [-d] [-D] page ...
man -c [-C file] [-d] [-D] page ...
man [-hV]
```
```

# Description

Man is the system's manual viewer; it can be used to display manual pages, scroll up and down, search for occurrences of specific text, and other useful functions. Each argument given to man is normally the name of a program, utility or function. The pages associated with each of these arguments are then found and displayed. A section number, if provided, will direct man to look only in that section of the manual. The default action is to search in all of the available sections, following a pre-defined order and to show only the first page found, even if pages exist in several sections.

# General Options

| Option | Description |
| :--- | :--- |
| -h, --help | Print a help message and exit. |
| -V, --version | Display version information and exit. |
| -C file, --config | Use configuration file *file* rather than the |