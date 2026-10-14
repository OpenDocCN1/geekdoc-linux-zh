# 6

# REDIRECTION

![](bbox=[0.35, 0.25, 0.65, 0.48])

In this lesson we are going to unleash what may be the coolest feature of the command line. It's called *I/O redirection*. The “I/O” stands for *input/output*, and with this facility you can redirect the input and output of commands to and from files, as well as connect multiple commands together into powerful command *pipelines*. To show off this facility, we will introduce the following commands:

+   - **cat** Concatenate files
+   - **sort** Sort lines of text
+   - **uniq** Report or omit repeated lines
+   - **grep** Print lines matching a pattern
+   - **wc** Print newline, word, and byte counts for each file
+   - **head** Output the first part of a file
+   - **tail** Output the last part of a file
+   - **tee** Read from standard input and write to standard output and files

# Standard Input, Output, and Error

Many of the programs that we have used so far produce output of some kind. This output often consists of two types.