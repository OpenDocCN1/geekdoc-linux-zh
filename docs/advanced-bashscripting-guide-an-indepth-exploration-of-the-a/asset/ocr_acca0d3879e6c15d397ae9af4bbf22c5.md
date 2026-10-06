# Advanced Bash–Scripting Guide

◆ column 3 = lines common to both.

The options allow suppressing output of one or more columns.

+   ◆ -1 suppresses column 1
◆ -2 suppresses column 2
◆ -3 suppresses column 3
◆ -12 suppresses columns 1 and 2, etc.

uniq
This filter removes duplicate lines from a sorted file. It is often seen in a pipe coupled with sort.

```
cat list-1 list-2 list-3 | sort | uniq > final.list
# Concatenates the list files,
# sorts them,
# removes duplicate lines,
# and finally writes the result to an output file.
```

The useful -c option prefixes each line of the input file with its number of occurrences.

```
bash cat testfile
This line occurs only once.
This line occurs twice.
This line occurs twice.
This line occurs three times.
This line occurs three times.
This line occurs three times.
```

```
bash$ uniq -c testfile
1 This line occurs only once.
2 This line occurs twice.
3 This line occurs three times.
```

```
bash sort testfile | uniq -c | sort -nr
3 This line occurs three times.
2 This line occurs twice.
1 This line occurs only once.
```

The sort INPUTFILE | uniq -c | sort -nr command produces a frequency of occurrence listing on the INPUTFILE file (the -nr options to sort cause a reverse numerical sort). This template finds use in analysis of log files and dictionary lists, wherever the lexical structure of a document needs to be examined.

# Example 12–9. Word Frequency Analysis

```
#!/bin/bash
# wf.sh: Crude word frequency analysis on a text file.

# Check for input file on command line.
ARGS=$1
E_BADARGS=65
```

# 12.4. Text Processing Commands