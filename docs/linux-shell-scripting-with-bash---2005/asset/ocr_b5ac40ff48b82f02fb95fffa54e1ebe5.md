A gauge is a thermometer bar showing the percentage progress. New percentages are read one at a time from standard input until the end of file is reached. The ~gauge switch requires a text message, the height, width, and an optional starting percentage (see Listing 13.2). The percentages can be sent to the gauge by a named pipe, discussed in Chapter 11, "Text File Basics."

Suppose you would like to show a thermometer graph showing the progress of printing a series of invoice files stored in a directory called invoices. The following demo displays the invoices as they are sent another script called print_invoice.

# Listing 13.2  **gauge_demo.sh**

```
#!/bin/bash
#
# gauge_demo.sh: a thermometer graph demo

shopt -s -o nounset

declare -rx SCRIPT=$({
declare -rx QUEUE=/status_fifo"
declare -rx INVOICES_DIR="invoices"
declare -ix TOTAL_INVOICES=0
declare -ix NUM_INVOICES=0
declare -ix PERCENT=0

# count the invoices waiting to print

TOTAL_INVOICES='ls -i $INVOICES_DIR | wc -1'

# create the pipe

mkfifo $QUEUE
if [ $? -ne 0 ] ; then
    printf *%s\n" "$SCRIPT:$LINENO: unable to create $QUEUE" >&2
    exit 192
fi

# print the invoices in a background subshell
# print the progress to the pipe

(
    ls -1 | (
        while read INVOICE ; do
            let "NUM_INVOICES++"
            print_invoice "$INVOICE"
            PERCENT=100*$NUM_INVOICES/$TOTAL_INVOICES
            printf *%d\n" "$PERCENT"
```