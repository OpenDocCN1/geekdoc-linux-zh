
# Advanced Bash-Scripting Guide

```bash
# Set variable to pass as parameter to "display" function.
avar=$(echo "${array[@]}") # Convert array to string variable.
display="$avar" # Display it.
echo;
echo "Generation $generation    $alive alive"
```

```bash
if [ "$alive" -eq 0 ];
then
    echo
    echo "Premature exit: no more cells alive!"
    exit $NONE_ALIVE    # No point in continuing
                      # if no live cells.
fi
```

```bash
# main ()
{
    # Load initial array with contents of startup file.
    initial=$(cat "$startfile" | sed -e '/#/d' | tr -d '\n')
    # Delete lines containing # comment character.
    sed -e 's/\//g' -e 's/\_/g'
    # Remove linefeeds and insert space between elements.
```

```bash
clear
echo # Title
setterm -reverse off
echo "$GENERATIONS generations"
echo "$of"
echo "*Life in the Slow Lane*"
setterm -reverse on
```

```bash
setterm -reverse off
sleep $DELAY # Display "splash screen" for 2 seconds.
```

```bash
# Display first generation.
Gen0=$(echo "${initial[0]}")
display="$Gen0" # Display only.
echo;echo
echo "Generation $generation    $alive alive"
sleep $DELAY
```

```bash
let generation += 1 # Bump generation count.
echo
```

```bash
# Display second generation.
Cur=$(echo "${initial[0]}")
next_gen="$Cur" # Update & display.
sleep $DELAY
```

Appendix A. Contributed Scripts

# Advanced Bash-Scripting Guide

```bash
let "generation += 1"      # Increment generation count.

# ----- Main loop for displaying subsequent generations -----
while [ "$generation" -le "$GENERATIONS" ]
do
  Cur=$Svar
  next_gen "$Cur"
  let "generation += 1"
  sleep $DELAY
done
#=====================================================

echo
)

exit 0      # EOF:EOF
```

```bash
# The grid in this script has a "boundary problem."
# The top, bottom, and sides border on a void of dead cells.
# Exercise: Change the script to have the grid wrap around,
#   so that the left and right sides will "touch",
#   as the top and bottom.
# Exercise: Create a new "gen0" file to seed this script.
# Use a 12 x 16 grid, instead of the original 10 x 1 one.
#   Make the necessary changes to the script,
#   so it will run with the altered file.
# Exercise: Modify this script so that it can determine the grid size
# from the "gen0" file, and set any variables necessary
#   for the script to run.
#   This would make unnecessary changes to variables
#   in the script for an altered grid size.
# Exercise: Optimize this script.
#   It has redundant code.
```

### A-11. Data file for Game of Life

```bash
gen0
# This is an "generation 0" start-up file for "life.sh".
# The "gen0" file is a 10 x 10 grid using a period (.) for live cells,
# and an underscore (_) for dead ones. We cannot simply use spaces
#   for dead cells in this file because of a peculiarity in Bash arrays.
#   [Exercise for the reader: explain this.]
```

# Lines beginning with a '#' are comments, and the script ignores them.

```
# ... (remaining lines omitted)
# (remaining lines omitted)
```

# Advanced Bash-Scripting Guide

The following script is by Mark Moraes of University of Toronto. See the file COPYRIGHT for permissions and restrictions. This file is included in the combined source tarball.

### Example A-12. Removing mail and news headers

```bash
#!/bin/sh
# Strips the header from mail message until the empty line.
# Author: Mark Moraes, University of Toronto.
# These comments added by author.

if [ $# -eq 0 ]; then
    # If no command-line arguments present, then work on stdin.
    sed -e '1,$d' -e '/$/d'
    # Delete empty lines and all lines until beginning with space
else
    # If command-line arguments present, then work on files.
    for i; do
        sed -e '1,$d' -e '/$/d' "$i"
        # Ditto, as above.
    done
fi

# Exercise: Error checking and other options.
# Note that the small script repeats, except for arguments passed.
# Does it make sense to embed it in a function? Why or not?
```

```
/*
* Copyright University of Toronto 1988-1989.
* Written by Mark Moraes
* Permission is granted to anyone to use this software for any computer system,
* to alter and redistribute it freely, subject to the following restrictions:
* 1. The author and University of Toronto are not responsible for the consequences of using this software, matter how awful they arise from it.
* 2. The origin of this software must not be misrepresented, either by explicit claim or omission. Since users ever read the sources, credits must appear in the documentation.
* 3. Altered versions must be marked as such, and must not be misrepresented as the original software. Since users ever read sources, credits must appear in the documentation.
* 4. This notice may not be removed or altered.
*/
```

# Advanced Bash-Scripting Guide

Antek Sawicki contributed the following script, which makes very clever use of parameter operators discussed in Section 10.2.

### Example A-13. Generating random 8-character passwords

```bash
#!/bin/bash
# Random password generator for Bash 2.x by Antek Sawicki tenox@tenox.tc,
# generously usage permission to author.
# Comments added by document author

MATRIX="0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz"
# Password will consist of alphanumeric characters.
LENGTH="8"
# May change 'LENGTH' for longer password.

while [ "$n" -le "$LENGTH" ]; do
    # Recall that := is "default substitution" operator.
    # So, if 'n' has not been initialized, set it to 1.
    :n:=1
    PASS=$PASS+${MATRIX:$((RANDOM%#MATRIX)):1}
    # Very clever, tricky.

    # Starting from the innermost nesting...
    # ${#MATRIX} returns length of array.
    # ${RANDOM%#MATRIX} returns random number between 0 and [length of MATRIX] - 1.

    # ${MATRIX:$((RANDOM%#MATRIX)):1} returns expansion of MATRIX at random position, by length 1.
    # See (var:pos:len) parameter substitution in Chapter 9 and the associated examples.

    # PASS=... simply pastes this onto previous PASS (concatenation).
    # To visualize this more clearly, uncomment the following line:
    # echo "$PASS"
    # to see PASS being built up one character at a time, each iteration of the loop.
    let n++
    # Increment 'n' for next pass.
done

echo "$PASS"
# Or, redirect to a file, as desired.
```

James R. Van Zandt contributed this script which uses named pipes and, in his words, "really exercises quoting and escaping."

### Example A-14.fifo: Making daily backups, using named pipes

```bash
#!/bin/bash
# Script by James R. Van Zandt, and used here with his permission.
# Comments added by author of this document.

HERE=$(uname -n) # hostname
THERE=bilbo
echo "starting remote backup to $HERE $(date +%r)"
# 'date +%r' returns time in 12-hour format, i.e. "08:08:34 PM"

# make sure /pipe really is a pipe and not a plain file
rm -rf /pipe
mkfifo /pipe # Create a "named pipe", named "pipe" ...

# 'su xyz' runs commands as user 'xyz'
# 'sh' invokes secure shell (remote login client).
su xyz -c "sh cat /home/xyz/backup/$HERE-daily.tar.gz" < /pipe & 
cd /
tar -czf - bin etc home lib main root share usr var > /pipe
# Used pipe, /pipe, to communicate between processes:
# => 'tar' writes to /pipe and 'ssh' reads from /pipe.

# What are the advantages of a "named pipe" in this situation,
# as opposed to an "anonymous pipe", with |
# Will an anonymous pipe even work here?

# Is it necessary to delete the pipe before exiting the script?
# How could that be done?

exit 0
```
