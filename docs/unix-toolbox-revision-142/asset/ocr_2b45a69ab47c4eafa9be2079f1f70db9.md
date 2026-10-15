# — Useful Commands —

+   - Ctrl-a c create an new window (terminal)
+   - Ctrl-a Ctrl-n and Ctrl-a Ctrl-p to switch to the next or previous window in the list, by number.
+   - Ctrl-a Ctrl-N where N is a number from 0 to 9, to switch to the corresponding window.
+   - Ctrl-a " to get a navigable list of running windows
+   - Ctrl-a a to clear a missed Ctrl-a
+   - Ctrl-a Ctrl-d to disconnect and leave the session running in the background
+   - Ctrl-a x lock the screen terminal with a password

The screen session is terminated when the program within the running terminal is closed and you logout from the terminal.

# 14.7 Find

Some important options:

+   -x (on BSD) -xdev (on Linux) Stay on the same file system (dev in fstab).
+   -exec cmd {} \; Execute the command and replace {} with the full path
+   -iname Like -name but is case insensitive
+   -ls Display information about the file (like ls -la)
+   -size n n is +-n (k M G T P)
+   -cmin n File's status was last changed n minutes ago.

```
# find . -type f ! -perm -444        # Find files not readable by all
# find . -type d ! -perm -111        # Find dirs not accessible by all
# find /home/user/ -cmin 10 -print    # Files created or modified in the last 10 min.
# find . -name "*. [ch]" | xargs grep -E 'expr' # Search 'expr' in this dir and below.
# find / -name "*.core" | xargs rm    # Find core dumps and delete them (also try core.*)
# find / -name "*.core" -print -exec rm {} \; # Other syntax
# Find images and create an archive, iname is not case sensitive. -r for append
# find . \( -iname "*.png" -o -iname "*.jpg" \) -print -exec tar -rf images.tar {} \;
# find . -type f -name "*.txt" ! -name README.txt -print # Exclude README.txt files
# find /var/ -size +10M -exec ls -lh {} \;    # Find large files > 10 MB
# find /var/ -size +10M -ls                    # This is simpler
# find . -size +10M -size -50M -print
# find /usr/ports/ -name work -type d -print -exec rm -rf {} \;  # Clean the ports
# Find files with SUID; those file are vulnerable and must be kept secure
# find / -type f -user root -perm -4000 -exec ls -l {} \;
```

Be careful with xarg or exec as it might or might not honor quotings and can return wrong results when files or directories contain spaces. In doubt use "-print0 | xargs -0" instead of "| xargs". The option -print0 must be the last in the find command. See this nice mini tutorial for find²².

```
# find . -type f | xargs ls -l        # Will not work with spaces in names
# find . -type f -print0 | xargs -0 ls -l  # Will work with spaces in names
# find . -type f -exec ls -l '{}' \;  # Or use quotes '{}' with -exec
```

# 14.8 Miscellaneous

```
# which command                     # Show full path name of command
# time command                       # See how long a command takes to execute
# time cat                            # Use time as stopwatch. Ctrl-c to stop
# set | grep $USER                    # List the current environment
# cal -3                              # Display a three month calendar
# date [+u][-utc][--universal] [MMDDhhmm[CC]YY[.ss]]
# date 10022155                       # Set date and time
# whatis grep                         # Display a short info on the command or word
# whereis java                        # Search path and standard directories for word
# setenv varname value                # Set env. variable varname to value (csh/tcsh)
# export varname="value"             # set env. variable varname to value (sh/ksh/bash)
# pwd                                 # Print working directory
# mkdir -p /path/to/dir               # no error if existing, make parent dirs as needed
# mkdir -p project/{bin,src,obj,doc/{html,man,pdf},debug/some/more/dirs}
# rmdir /path/to/dir                  # Remove directory
```