# Chapter 3: Compound Command Syntax 153

hello
again
$

The cat command at the end of the second command line in this and the previous question could have been given on separate command lines, but doing it way illustrates that the redirection applies to the grouped commands, not to the entire command line.

![](bbox=[0.903, 0.188, 0.981, 0.233])

Inside braces, pipe the output of cat to tr a-z A-Z and redirect stdin for the entire pipeline to come from your days of the week file. Do the same thing with parentheses.

+   c) Did the days go to the cat command or to the tr command?
Answer:Your interaction should look like the following:
$ ( cat | tr a-z A-Z ) < days
SUNDAY
MONDAY
TUESDAY
WEDNESDAY
THURSDAY
FRIDAY
SATURDAY
$ ( cat | tr a-z A-Z ) < days
SUNDAY
MONDAY
TUESDAY
WEDNESDAY
THURSDAY
FRIDAY
SATURDAY
$

Because tr gets its input from the output of cat, using the pipeline connector (| |), it must be that days went to the first command in the pipeline, the cat command.

Run this command line:
{ print hello; cat;} < days

+   d) How do you interpret the output you see?
Answer:Your interaction should look like the following:
$ ( print hello; cat;) < days