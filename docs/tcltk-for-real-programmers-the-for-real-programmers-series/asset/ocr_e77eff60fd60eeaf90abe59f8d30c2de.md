# 10.3 Text Widget Subcommands

# Script Output

| ID DATA INDEX |
| tagon TAG1 1.0 |
| text This text is tagged 'TAG1'. 1.0 |
| tagoff TAG1 1.29 |
| tagon TAG2 1.29 |
| text This is on the same line, 'TAG2' 1.29 |
| tagoff TAG2 2.0 |
| tagon INSERTED 2.0 |
| text Line 2 becomes line 3 when this is inserted at 2.0 2.0 |
| tagoff INSERTED 3.0 |
| text The linefeed after 'TAG2' puts this on a new line. 3.0 |
| mark 4.0 |
| mark current 4.0 |

# Script Results

![](bbox=[0.148, 0.445, 0.822, 0.532])

In the previous example, all the lines are shorter than the width of the text widget. Since none of the lines wrap, the text is displayed on the same line as the internal representation.

The first line of the example inserted a line with the text This is tagged 'TAG1' at the end of the text widget. Since there was no text in the widget, the end was also the beginning at point.

The dump shows that tag TAG1 starts at index 1.0 and ends at index 1.29. The text also starts at index 1.0.

Note that the second set of text is also inserted onto line 1. This is because the first set of inserted text did not have a newline character to mark it as terminating a line.

The second set of text has a newline character at the end, which causes the next line to be inserted at index 2.0.