instead of being displayed on the screen.

**filter** Filters are a particular type of Unix program that expects to work either with file redirection or as part of a pipeline. These programs read input from standard input, write output to standard output, and often don’t have any starting arguments.

**inclusion range** This is a range of characters that a pattern must include.

**left-rooted** Patterns that must occur at the beginning of a line are said to be left-rooted.

**regular expression** This is a convenient notation for specifying complex patterns. Notable special characters are ^ to match the beginning of the line and $ to match the end of the line.

**standard error** This is the same as standard output, but you can redirect standard error to a different location than standard output.

**standard input** Unix programs always default to reading information from the user by reading the keyboard and watching what’s typed. With file redirection, input can come from a file, and with pipelines, input can be the result of a previous Unix command.

**standard output** When processing information, Unix programs default to displaying the output on the screen, also known as standard output. With file redirection, output can easily be saved to a file; with pipelines, output can be sent to other programs.

**wildcards** Wildcards are special characters that are interpreted by the Unix shell or other programs to have meanings other than the characters themselves. For example, * is a shell wildcard and creates a pattern that matches zero or more characters. When prefaced, for example, with the letter X (X*), this shell pattern will match all files beginning with X.

# Exercises

+   1. The placement of file-redirection characters is important to ensure that a command works correctly. Which of the following do you think will work, and why?

[Click here to view code image](#)

```
    < file | wc       wc file <       wc < file
    cat file | wc      cat < file | wc   wc | cat
```

Now try them and see whether you’re correct.

+   2. Does the file size listed by `wc -c` always agree with the file size listed by the `ls` command? With the size indicated by `ls -s`? If there is any difference, why?

+   3. What do you think would happen if you tried to sort a list of words by pretending they’re all numbers? Try it with the command `ls -1 | sort -n` to see what happens. Experiment with the variations.

+   4. What wildcard expression would you use to find the following?
+   
+   - All files in the `/tmp` directory
+   - All files that contain a `w` in that directory
+   - All files that start with a `b`, contain an `e`, and end with `.c`