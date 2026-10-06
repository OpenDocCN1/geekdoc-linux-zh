
# Advanced Bash–Scripting Guide

◆ column 3 = lines common to both.

The options allow suppressing output of one or more columns.

- ◆ -1 suppresses column 1
- ◆ -2 suppresses column 2
- ◆ -3 suppresses column 3
- ◆ -12 suppresses columns 1 and 2, etc.

## uniq
This filter removes duplicate lines from a sorted file. It is often seen in a pipe coupled with sort.

```bash
cat list-1 list-2 list-3 | sort | uniq > final.list
# Concatenates the list files,
# sorts them,
# removes duplicate lines,
# and finally writes the result to an output file.
```

The useful -c option prefixes each line of the input file with its number of occurrences.

```bash
bash cat testfile
This line occurs only once.
This line occurs twice.
This line occurs twice.
This line occurs three times.
This line occurs three times.
This line occurs three times.
```

```bash
bash$ uniq -c testfile
1 This line occurs only once.
2 This line occurs twice.
3 This line occurs three times.
```

```bash
bash sort testfile | uniq -c | sort -nr
3 This line occurs three times.
2 This line occurs twice.
1 This line occurs only once.
```

The `sort INPUTFILE | uniq -c | sort -nr` command produces a frequency of occurrence listing on the INPUTFILE file (the -nr options to sort cause a reverse numerical sort). This template finds use in analysis of log files and dictionary lists, wherever the lexical structure of a document needs to be examined.

## Example 12–9. Word Frequency Analysis

```bash
#!/bin/bash
# wf.sh: Crude word frequency analysis on a text file.

# Check for input file on command line.
ARGS=$1
E_BADARGS=65
```

## 12.4. Text Processing Commands

```bash
E_NOFILE=66

if [ $# -ne "$ARGS" ]; then # Correct number of arguments passed to script?
then
    echo "Usage: `basename $0 filename`"
    exit $E_BADARGS
fi

if [ ! -f "$1" ]; then # Check if file exists.
then
    echo "File\$1" does not exist.\n
    exit $E_NOFILE
fi
```

```bash
############################################################
# main ()
sed -e 's/\.'//g' -e s/ | -c/g "$1" | tr 'A-Z-a-z' | sort | uniq | sort -nr
############################################################
    Frequency of occurrence

# Filter out periods and
+# change space between words to linefeed,
+# then shift characters to lowercase, and
+# finally prefix occurrence count and sort numerically.
############################################################
# Exercises:
# 1) Add 'sed' commands to filter out other punctuation, such as commas.
# 2) Modify to filter multiple spaces and other whitespace.
# 3) Add a secondary sort key, so that instances of equal occurrence
+# are sorted alphabetically.
```

```bash
bash$ cat testfile
This line occurs once.
This line occurs twice.
This line occurs twice.
This line occurs three times.
This line occurs three times.
This line occurs three times.
```

```bash
bash$. ./wf.sh testfile
6 this
6 occurs
6 line
3 times
3 three
2 twice
1 only
1 once
```

### expand, unexpand

The expand filter converts tabs to spaces. It is often used in a pipe.

## 12.4. Text Processing Commands

The unexpand filter converts spaces to tabs. This reverses the effect of expand.

### cut

A tool for extracting fields from files. It is similar to the print $N$ command in awk, but more limited. It may be simpler to use cut in a script than awk. Particularly important are the -d (delimiter) and -f (field specifier) options.

Using cut to obtain the list of mounted filesystems:

```bash
cat /etc/mtab cut -d ' ' -f1,2
```

Using cut to list the OS and kernel version:

```bash
uname -a | cut -d" " -f1,3,11,12
```

Using cut to extract headers from an e-mail folder:

```bash
bash grep '^Subject:' messages | cut -c10-80
Subject: Linux for mission-critical apps
Subject: Spam
```

Using cut to parse a file:

```bash
# List all the users in /etc/passwd
FILENAME=/etc/passwd

for user in $(cut -d: -f1 $FILENAME)
do
    echo $user
done
# Thanks for suggesting this.
```
`cut -d ' ' -f2,3` is equivalent to awk -F' ' '{print $2,3}'.

### join

Tool for merging different files into a single multi-column file. In combination with cut, useful for creating system files. Consider this a special-purpose cousin of paste. This powerful utility allows merging two files in a meaningful fashion, which creates a simple version of a relational database. The join command operates on exactly two files, but pastes together those lines with a common tagged field (usually numerical), and writes the result to stdout.

| range | action |
|---|---|
| 1.data | 2.data |
| 100 | Shoes |
| 200 | Laces |
| 300 | Socks |

```bash
bash$ join 1.data 2.data
File: 1.data 2.data
100 Shoes
200 Laces
300 Socks
```

The tagged field appears only once in the output. head lists the beginning of a file to stdout (the default is 10 lines, but this can be changed). It has a number of interesting options.

## Example 12–10. Generating 10-digit numbers

```bash
#!/bin/bash
# rnd.sh: Outputs 10-digit random number
# Script by Stephane Chelas.
head -c4 /dev/urandom | od -N4 -tu4 | sed -ne '1s/..*//p'

# =================================================
# head:
# -c4 option takes first 4 bytes.

# od:
# -N4 option limits output to 4 bytes.
# -tu4 option selects unsigned format for output.

# sed:
# -n option, in combination with "p" flag to "s" command,
# outputs only matched lines.
```

```bash
# The author of this script explains the action of 'sed', as follows.

# head -c4 /dev/urandom | od -NA -tu4 | sed -ne '1s/..*//p'
# Assume output to "sed" -> is 0000000 198154

# sed begins reading characters: 0000000 198154n.
# Here it finds a newline character,
# so it is ready to process the first line (0000000 198154n).
# It looks at its range-$s. The first and only one is:

| range | action |
|---|---|
| 1 | s.// |

# The text line is in the range, it executes the action:
# tries to substitute the longest string with a space in the line
# ("0000000" with nothing (//), and if it succeeds, prints the result
# (*p is a flag to the "s" command, which is different from the "p" command
# sed is now ready to continue reading its input. (Note that before
# continuing, if -n option had not been passed, sed would have printed
# the line once).

# Now, sed reads the remainder of the characters, and finds the end of the file.
# It is now ready to process its second line (which is also numbered '$') as
# it's the last one.
# it sees no matched by <range>, so its job is done.

# In this sed command means:
# "On the first line only, remove any character up to the right-most space,
# then print it."

# A better way to do this would have:
# sed -e '$s/. //q'

# Here, two range-$s (could have been written sed -e '$s.*/' -e q):

| range | action |
|---|---|
| nothing (matches line) | s.// |
| nothing (matches line) | q (quit) |

# sed, only reads its first line of input. (substituted) before quitting
# It performs both actions, and prints the line (because of the "q" command)
# since the "-n" option is not passed.

# A simpler alternative to the above 1-line script would be:
# head -c4 /dev/urandom od -An -tu4

exit 0
```

See also Example 12–28.

## 12.4. Text Processing Commands

lists the end of a file to stdout (the default is 10 lines). Commonly used to keep track of changes to the system log, using the -f option, which outputs lines appended to the file.

## Example 12–11. Using tail to monitor the system log

```bash
#!/bin/bash
filename=sys.log

cat /dev/null $filename; echo "Creating cleaning out file."
# Creates file if it does not exist,
# truncates it to zero length if it does.
# > filename also works.

tail /var/log/messages $filename
# /var/log/messages must have read permission for this to work.
echo "$filename contains tail end of system log."
exit 0
```
