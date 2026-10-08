# Advanced Bash-Scripting Guide

## directories for which you have read permissions. you can't
## read is not in the list.

# ABS Guide advises caution when running scripts as root:

########## THIS IS CONFIGURABLE ##########

```
TOP=5 # Top 5 biggest. (sub)directories.
MAXRECURS=5 # Max 5 subdirectories/cursions deep.
E_BL=80 # Blank line already returned.
E_DIR=81 # Directory not specified.
```

########## DON'T CHANGE ANYTHING BELOW THIS LINE #

```
PID=$$ # Our own process ID.
SELF=$(basename $0) # Our program name.
TMP=$(tmp/$(SELF)).$(PID).tmp # Temporary 'du' result.
```

```
# Convert number to thousand.
$***
function dot { echo $1 | sed -a 's/\.[0-9]*\([0-9]\{3}\)/\1,\2;;ta'
tail -c 12; }
```

```
# Usage: tree <recursion> <indent prefix> <min size> <directory>
function tree {
curs=$1 # How deep nested are we?
prefix=$$2 # What do we display before file/dirname?
minsize=$$3 # What is the minimum file/dirsize?
dirname=$$4 # Which directory are we creating }
```

```
# Get (TOP) biggest subdirectories/subfiles from TMP file.
LIST=$(grep '^[[:space:]]*$(dirname)/.*' "$TMP'
awk '{if($1)}print $0}' | sort -nr | head -$TOP
-z "$LIST" && return 4 # Empty list, then go back.
```

```
cnt=0
um=$(echo "$LIST" | wc -l) # How many entries in the list.
```

```
# Main loop
echo "$LIST" | while read dirname; do
((cnt++)) # Count entry number.
basename=$(basename "$") # We only need a basename of the entry.
d -d "$basename" && basename="$basename/" # If it's a directory, append slash.
echo "dot $basename" # Display the result.
```

```
# Call recursively too if it's a directory
+# and we're not too deep $(MAXRECURS).
The recursion goes up: $(curs+1)
+# prefix gets a space if it's the last entry,
+# or a pipe if there are more entries.
The minimum file/dirsize becomes $(((minsize/10))).
# Last argument is the full directory name to check.
if [ -d "$dirname" -a recurs -lt $MAXRECURS ]; then
 [[ $cnt -lt $num ]] && \
 | tree $((curs+1)) "$prefix | $((minsize/10)) "$name" \
& && tree $((curs+1)) "$prefix | $((minsize/10)) "$name" )
```

done

# Appendix A. Contributed Scripts

600