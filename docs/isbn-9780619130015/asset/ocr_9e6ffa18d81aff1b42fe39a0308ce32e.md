![](bbox=[0.15, 0.08, 0.76, 0.41])

Figure 9-10: Output of example9.p

Now that you understand about data types, you are ready to learn more about programming using Perl. Perl's similarities and differences with other programming languages can be illustrated by comparing how the same program appears in awk and Perl.

# ## Perl versus Awk Programs

Awk does not require the programmer to explicitly set up looping structures as Perl does. Perl's while loop, on the other hand, is almost identical to the one found in C and C++. Awk, therefore, uses fewer lines of code to resolve pattern-matching extractions than Perl does. For example, look at the following awk program, awkcom.a, and its output. The program counts the number of comment lines that appear in the file specified on the command line.

```
!usr/bin/awk -f
# program name: awkcom.a
# purpose: Count the comment lines in a file
#
Enter the filename on the command line.

END {
	print "The file has ", line_count, " comment lines."
}
/"^#`/ " !/^#!`/ { ++line_count } # This occurs for every line.

```