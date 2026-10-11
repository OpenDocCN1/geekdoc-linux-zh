Statistics not relevant to your hardware are shown as zero.

```
$ command time grep ken /etc/aliases
Command exited with non-zero status 1
0.00user  0.00system  0:00.02elapsed  0%CPU  (0avgtext+0avgdata 0maxresident)k
0inputs+0outputs (142major+19minor)pagefaults 0swaps
$ command time --format "%P" grep ken /etc/aliases
Command exited with non-zero status 1
0%
$ command time --format "Major faults = %W" grep ken /etc/aliases
Command exited with non-zero status 1
Major faults = 141
```

The `--portability` (-p) switch forces time to adhere to the POSIX standard, the same as Bash time -p, turning off many of the extended features.

```
$ command time --portability grep ken /etc/aliases
Command exited with non-zero status 1
real  0.00
user  0.00
sys  0.00
```

The results can be redirected to a file with `--output` (-o), or appended to a file with `--append` (-a). The `--verbose` (-v) option gives a detailed explanation of each statistic.

# # Creating Man Pages

Linux man pages are special text files formatted for the groff program (GNU run off). groff is based on the older Unix programs troff (for printers) and nroff (for terminals). Troff was originally created in 1973 by Joseph E Ossanna. By creating short man pages for important scripts, a single access point can be created for online information about your projects.

Place man pages for your own projects in section 9 of the manual. Originally, section 9 was used to document the Linux kernel, but it now follows the traditional Unix interpretation as being free for your personal use. Manual pages for section 9 are usually stored in /usr/share/man/man9. If you don't have access to this directory, make a man9 directory your home directory and store your personal manual pages there. By adding $HOME to the MANPATH environment variable in your Bash profile file, man will search the pages stored in your man9 directory.

```
$ mkdir ~/man9
$ declare -x MANPATH="$HOME:/usr/share/man "
```

man pages are text files containing groff markup codes (or macros) embedded in the text. These codes, much like HTML tags in a Web page, control the spacing, layout, and graphics used in the pages. You can also define your own groff codes. These codes always appear at the start of a line and begin with a period.