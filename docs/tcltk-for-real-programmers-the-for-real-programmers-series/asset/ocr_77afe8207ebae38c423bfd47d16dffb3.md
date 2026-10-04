```
####################################################################
# proc Hmtag_/table {win param text}---
# Process the </TABLE> tag
# This procedure resets the window to receive text to the
# master window.
# Arguments
#
# table      The window that holds the table
# param      Any parameters in the <TABLE ...> tag
# text       The name of a variable with associated text
#
# Results
# Maps the new window into the master text window.
# Sets tab locations in new window

proc Hmtag_/table {table param text} {
    global HMtable

    # Set the var pointer for the table text widget
    upvar var #0HMtable var

    # Set the win and var variables to point to the master text
    # widget, instead of the table text widget.
    set win $var(oldWindow)
    upvar #0 HMSwin var

    # unset var(divert) so that text will no longer be diverted
    # to the table window
    unset var(divert)

    # Reset the height of the table text widget to match the
    # number of rows actually used and insert it into the
    # master text widget
    $table configure -height $HMtable(row) -font $var(xfont)
    $win create $var(S_insert) -window $table

    # The next pieces of code set the tab stops to define
    # the columns in the table.
    # First determine the widest entry in each column.
    # Initialize the sizes for the columns to 0
    for {set j 0} {$j < $HMtable(maxCol)}{incr j} {
```