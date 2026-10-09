# Table 9-13 bash features

| Feature | Description | Syntax | Alternate syntax |
|---|---|---|---|
| **allexport** | Automatically places in the environment (exports) all variables and functions you create or modify after giving this command (default is off). | **set -o allexport** | **set -a** |
| **braceexpand** | Causes *bash* to perform brace expansion (default is on; page 405). | **set -o braceexpand** | **set -B** |
| **cdspell** | Corrects minor spelling errors in directory names used as arguments to *cd* (default is off). | **shopt -S cdspell** |  |
| **cmdhist** | Saves all lines of a multiline command in the same history entry, adding semicolons as needed (default is on). | **shopt -S cmdhist** |  |
| **dotglob** | Causes shell special characters (wildcards; page 165) in an ambiguous file reference to match a leading period in a filename. By default, special characters do not match a leading period: You must always specify the filenames `.` and `..` explicitly because no pattern ever matches them (default is off). | **shopt -S dotglob** |  |
| **emacs** | Specifies *emacs* editing mode for command-line editing (default is on; page 387). | **set -o emacs** |  |
| **errexit** | Causes *bash* to exit when a pipeline (page 158), which can be a simple command (page 147; not a control structure), fails (default is off). | **set -o errexit** | **set -e** |
| **execfail** | Causes a shell script to continue running when it cannot find the file that is given as an argument to *exec*. By default, a script terminates when *exec* cannot find the file that is given as its argument (default is off). | **shopt -S execfail** |  |
| **expand_aliases** | Causes aliases (page 392) to be expanded (default is on for interactive shells and off for noninteractive shells). | **shopt -S expand_aliases** |  |
| **hashall** | Causes *bash* to remember where commands it has found using *PATH* (page 359) are located (default is on). | **set -o hashall** | **set -h** |