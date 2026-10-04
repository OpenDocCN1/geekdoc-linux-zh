| sequence-start? | sequence-end? | sequence-index | sequence-item |
|---|---|---|--|
| 1 | 0 | 0 | Henderson |
| 0 | 0 | 1 | Jackson |
| 0 | 0 | 2 | Johnson |
| 0 | 0 | 3 | Jones |
| 0 | 0 | 4 | King |
| 0 | 1 | 5 | Smith |

Figure 4-7: The output of the code to iterate elements and display them in a table

The in tag defines several variables with which you carry out calculations on the sequence elements and allow the batch processing of sequences. This can be very useful in the case of long sequences that are better displayed in several small batches instead of all at once.

See Appendix A for a list of summary and statistics variables, special element grouping variables, and batch processing variables.

# 4.3.10.1 Count Loops Using the in Tag

Another useful function of the in tag is its ability to repeatedly execute code. To do this, the in tag uses the range method, which can accept a maximum of three arguments:

> range(Startvalue, Endvalue, Interval)

If only one argument is specified, the argument is the end value, the start value is zero, and the interval is 1. Using this method a list of the numbers is created, and the resulting list can be run through the in tag. For example, calling up range(5) creates a five-element list [0, 1, 2, 3, 4] so that you can use the in tag to define a loop to run the actions five times.

The following causes the line "Hello!" to be inserted ten times in the rendered output of a document:

```
<html-in "_.range(10)"><br>
Hello!<br>
</html-in>
```