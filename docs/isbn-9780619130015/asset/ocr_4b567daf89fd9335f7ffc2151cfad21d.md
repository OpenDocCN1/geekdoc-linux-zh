# **To create a script and add comments:**

+   **1** After the $ command prompt, type vi pact and press Enter.
**2** Type a to switch to insert mode, and then type the text below, pressing Enter at the end of each line:

```
```
# ================================================
# Script Name: pact
# By: Instructor
# Date: November 1999
# Purpose: Create temporary file, pnum, to hold the
# count of the number of projects each
# programmer is working on. The pnum file
# consists of
# prog_num and count fields
# ================================================
cut -d: -f4 project | sort | uniq -c |
awk '{printf "%s:%s\n",$2, $1}' > pnum
# cut prog_num, pipe output to sort to remove duplicates
# and get count for prog/projects.
# output file with prog_number followed by count
```
```

+   **3** Press Esc to switch to command mode.
**4** Type :wq to write the file and exit from vi.

Now you can run pact and use the less command to display the contents of pnum.

Note: The shell scripts in the following steps are executed using the sh command.

# **To run the script:**

+   **1** After the $ command prompt, type sh pact and press Enter.
**2** Type less pnum and press Enter.
**3** You see these programmer numbers and count fields:

```
```
101:1
102:2
103:2
104:1
105:2
106:1
107:1
109:1
110:2
112:1
```
```