
A while loop is completed with the `done` command, not `elihw` as you might expect.
An *infinite* loop can be created using the `true` command. Because `true` always succeeds, the loop will continue indefinitely.

```bash
printf "%s\n" "Enter the names of companies or type quit"
while true ; do
    read -p "Company ?"  COMPANY
    if [ "$COMPANY" = "quit" ] ; then
        break
    elif test -f "orders_$COMPANY.txt" ; then
        printf "%s\n" "There is an order file from this company"
    else
        printf "%s\n" "There are no order files from this company"
    fi
done
```

A while loop can be stopped prematurely with the `break` command. On reaching a break, Bash stops executing commands and “breaks out” of the loop and begins executing the *first* command *after* the loop.
`break` can be followed by a number indicating how many enclosing loops to break out of. For example
`break 2` breaks out of the current loop as well as the loop enclosing the current loop.
The counterpart to `break` is `continue`, which causes the remainder of the enclosed statements to be ignored; the loop is resumed at the top. `continue` can be followed by a number indicating how many enclosing statements to break out of before continuing.

### until Loop

The counterpart of the while loop is the `until` loop. The `until` command is identical to the `while` command except that it repeats the enclosed statements until the condition is *successful*, essentially the same as `while !`.

```bash
until test -f "$INVOICE_FILE" ; do
    printf "%s\n" "Waiting for the invoice file to arrive..."
    sleep 30
done
```

Using `until` with the `false` command creates an infinite loop.
The `break` and `continue` commands can be used with an `until` loop.

### for Loops

The standard Bourne `for in loop` is a variation on the here file. The `for` command reads a sequence of values into a variable and repeats the enclosed commands once for each value.

```bash
for FILE_PREFIX in order invoice purchase order; do
    if test -f "$FILE_PREFIX"_vendor1.txt" ; then
        printf "%%s\n" "There is a $FILE_PREFIX file from vendor l..."
    fi
done
```

If the `in` part is missing, the `for` command will execute the enclosed statements for each argument to the shell script.

The `break` and `continue` commands can be used with a `for` loop.

Because of the other shell features, this kind of `for` loop isn't commonly used.

### Embedded let( ( . . . ) )

The `let` command returns a status code of 1 if an expression is zero, or 0 if the expression is a value other than zero. In the same way that the `test` command can be expressed with a pair of square brackets for easier reading in compound statements, the `let` command also has a form for easier reading: double parentheses.

The `for` loop, as found in other programming languages, is created using an embedded `let`, as shown in Listing 7.1.

**Listing 7.1 forloop.sh**

```bash
#!/bin/bash
# forloop.sh: Count from 1 to 9
for (( COUNTER=1; COUNTER<10; COUNTER++ )) ; do
    printf "The counter is now %d\n" $COUNTER
done
exit 0
```

The first expression in the double parentheses is executed when the loop is started. Each time the loop is restarted, the third expression is executed and the second expression is checked. When the second expression returns `false`, the loop ends.

```bash
$ bash forloop.sh
The counter is now 1
The counter is now 2
The counter is now 3
The counter is now 4
The counter is now 5
The counter is now 6
The counter is now 7
The counter is now 8
The counter is now 9
```

### Grouping Commands ( {...} )

Commands can be grouped together using curly braces ( {...} ).

```bash
ls -1 | {
    while read FILE ; do
        echo "$FILE"
    done
}
```

In this example, the results of the `ls` command become the input for all the statements in the group.

```bash
$ test -f orders.txt && { ls -l orders.txt ; rm orders.txt; } \
    || printf "no such file"
```

If the file `orders.txt` exists, the file will be listed and deleted; otherwise, “no such file” is printed. The semicolon after the last braced command is required only when the braces are on a single line.

Commands can also be grouped using subshells. Subshells are described in Chapter 9, “Parameters and Subshells.”

### report.bash: Report Formatter

report.bash is a script that reads a list of sales figures and creates a simple report. The sales figure file consists of product names, local country sales, and foreign country sales. For example, report.bash turns this:

```text
binders 1024 576
pencils 472 235
rules 311 797
stencils 846 621
```

into the following report:

```text
Report created on Thu Aug 22 18:27:07 EDT 2002 by kbutrch

Sales Report
```

| Product   | Country | Foreign | Total | Average |
|:----------|--------:|--------:|------:|--------:|
| binders   |     1024|      576|   1600|       800|
| pencils   |      472|      235|    707|       353|
| rules     |      311|      797|   1108|       554|
| stencils  |      846|      621|   1467|       733|

Total number of products: 4

End of report

### Listing 7.2 report.bash

```bash
#!/bin/bash
#
# report.bash: simple report formatter
#
# Ken O. Burtch
# CVS: $header$
#
# The report is read from DATA_FILE. It should contain
# the following columns:
#
# Column 1: PRODUCT = Product name
# Column 2: CSALES = Country Sales
# Column 3: PSALES = Foreign Sales
#
# The script will format the data into columns, adding total and
# average sales per item as well as a item count at the end of the
# report.

# Some Linux systems use USER instead of LOGNAME
if [ -z "$LOGNAME" ] ; then # No login name?
declare -rx LOGNAME="$USER" # probably in USER
fi
shopt -s -o nounset

# Global Declarations

declare -rx SCRIPT=$0###/ # SCRIPT is the name of this script
declare -rx DATA_FILE="report.txt" # this is raw data for the report
declare -i ITEMS=0 # number of report items
declare -i LINE_TOTAL=0 # line totals
declare -i LINE_AVG=0 # line average
```

**Listing 7.2 Continued**

```bash
declare PRODUCT        # product name from data file
declare -i CSALES         # country sales from data file
declare -i FSALES          # foreign sales from data file
declare -rx REPORT_NAME="Sales Report" # report title
# Sanity Checks

if test ! -r "$DATA_FILE" ; then
       printf "$SCRIPT: the report file is missing-aborting\n" >&2
       exit 192
fi

# Generate the report

printf "Report created on %s by %s\n" "$DATE" "$LOGNAME"
printf "\n"
printf "%s\n" "$REPORT_NAME"
printf "\n"
printf "%-12s12s12s12s12s\n" "Product" "Country" "Foreign" "Total" "Average"
printf "%-12s12s12s12s12s\n" "___" "___" "___" "___" "___"

{ while read PRODUCT CSALES FSALES ; do
      let "ITEMS+=1"
      LINE_TOTAL=$(CSALES+FSALES)
      LINE_AVG=$((CSALES+FSALES)/2)
      printf "%-12s12d12d12d12d\n" "$PRODUCT" "$CSALES" "$FSALES" \
      "$LINE_TOTAL" "$LINE_AVG"
done } < $DATA_FILE
# Print report trailer

printf "%-12s12s12s12s12s\n" "___" "___" "___" "___" "___"
printf "Total number of products: %d\n" "$ITEMS"
printf "\n"
printf "End of report\n"

exit 0
```

# 8 Debugging and Version Control

WHEN I WAS IN BROCK UNIVERSITY, the Macquarrie lab was filled with used Macintosh Plus computers passed down from professors who had outgrown them. One day I was working on a program for my third-year operating system course. The short C program I was working on was reported to be error free. When I ran it, vertical bars appeared on the monochrome desktop, my floppy disk ejected, and the computer rebooted. Upon closer inspection, I noticed that I used an `!=` instead of a `==` in an `if` statement. That small mistake created unforeseen results. Ever since then, I treat the C language as a psychotic roommate; we might live and work together, but I never take my eye off it for a minute in case it tries to stab me in the back.

Unfortunately, shell scripts are almost as difficult to debug as C programs. Like C, shell commands usually assume you know what you are doing and issue an error only when the offending line actually runs. Unless shell scripts are thoroughly tested, bugs can linger for months or years until the faulty command is finally executed. A solid knowledge of shell debugging tools is essential for professional script development.

### Shell Debugging Features

There are several Bash switches and options useful in tracking down problems in scripts.

The `-n` (*no execution*) switch checks a script for syntax errors without running it. Use this switch to check a script during development.

```bash
$ bash -n bad.sh
bad.sh: line 3: syntax error near unexpected token `fi`
bad.sh: line 3: `fi'
```

In this example, there is an error on or before line 3 of the script. The term *token* refers to a keyword or another piece of text near the source of the error.

The `-o errxit` option terminates the shell script if a command returns an error code. The exceptions are loops, so the `if` command cannot work properly if commands can't return a non-zero status. Use this option only on the simplest scripts without any other error handling; for example, it does not terminate the script if an error occurs in a subshell.
