# Command-Line Interpreter

You can manually run the perl interpreter program directly from the command line to process a Perl script. To demonstrate this, let’s first create a simple Perl script to run. Here’s an example of a simple script to use:

```
$ cat test1.pl
# This is a test Perl script
print "This is a test.\n";
$
```

This two-line script incorporates a comment line (the line starting with a pound sign), which is ignored by Perl, and a single line of Perl code. The print command sends a string to the default standard output, which is the console when running interactively, such as from the Terminal program in Ubuntu (see Chapter 19, “The Ubuntu Command Line”).

The \n character at the end of the string represents a carriage-control character, allowing the cursor to move to the next line on the display. In shell scripts, the echo command (see Chapter 25) automatically adds the carriage-control character when displaying text. The Perl print command requires that you manually add the carriage-control character, which is a subtle difference that many programmers forget!

After saving the test1.pl file, you can run it from the command-line interface using the perl interpreter:

```
$ perl test1.pl
This is a test script.
$
```

When using the perl interpreter, you can also invoke several command-line options to control the behavior of the interpreter. The most popular options are -w, which produces warnings about any errant syntax in your Perl code, and -d, which runs the script within the Perl debugger:

```
rich@testing:~> perl -d test1.pl

Loading DB routines from perl5db.pl version 1.3
Editor support available.

Enter h or 'h h' for help, or 'man perldebug' for more help.

main::(test1.pl:1): print "This is a test script\n";
DB<1>
```

The debugger allows you to interactively step through the Perl script line by line, examining the results as each statement is executed. This is extremely handy when trying to find a bug in a large script.