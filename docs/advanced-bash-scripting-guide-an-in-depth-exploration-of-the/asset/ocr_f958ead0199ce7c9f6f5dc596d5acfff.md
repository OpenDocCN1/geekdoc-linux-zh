# Advanced Bash-Scripting Guide

Thus the script looks something like this:

###############################################################
# CD Setup                                                     
###############################################################
CDLPROMPTL=21      # Allow a prompt length of up to 21 characters
  /usr/bin/cdll      # Initialise cdll
alias s=$cd_new\ @  # Allow @ at the prompt to display history
cd -U               # Upload directories
cd -D               # Set default action to non-posix
###############################################################

The full meaning of a couple of caveats will become clear later. If another program changes the directory without calling cdll, then the directory won't be put on the stack and also if the prompt facility is used then this will not be updated. Two programs that can do is pushd and popd. To update the prompt and stack simply enter:

```
cd
```

Note that if the previous entry on the stack is the current directory then the stack is not updated.

Usage
=====
cd [dir] [0-9] [@sh] [-g <dir>] [-d] [-D] [-r<n>]
cd [0-9] [-R<n>] [<dir>:0-9] [-s<n>] [-S<n>]
[-u] [-U] [-f] [-F] [-h] [-V]

```
<dir>          Go to directory
O-n             Goto previous directory (0 is previous,
                               1 is last 1, etc.)
@               n is up to max history (Usually available as $)
@h              List history and special entries
@s              List special entries:
-<dir>          Go to literal names (bypass special names)
                This is to allow to access cdir '0','1',''h' etc
-d             Change default action verbose. (See note)
-D             Change default silent. (See note)
-S<n>           Go to the special entry
-S<n>           Go to the special entry <n>
                and replace it with the current dir
-r<dir>         Go to directory <dir>
                and then put it on special entry <n>
-R<n> [<dir>]     Go to directory <dir>
                and put cur on special entry <n>
-a<n>           Alternative suggested directory. See below.
-f <file>       Enter files to <file>
-u <file>       Update entries from <file>.
                If no filename then default file (~cdfile) is used
-F and -u are silent versions
-v              Print version number
-h              Help
-H              Detailed help
```

Appendix A. Contributed Scripts

696