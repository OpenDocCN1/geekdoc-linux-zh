
## Command-Line Interpreter

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

## Creating a Perl Program

The automatic method of running Perl scripts is accomplished by directly defining the Perl interpreter within the script itself. This uses the same technique we used in creating shell scripts to define the shell (see Chapter 25).

The first line in a Perl script must tell the shell what program to run to process the commands. For Perl, just as in the command-line method, this is the Perl interpreter program, which is located in the /usr/bin folder. After you define the Perl program in the script, you can enter the Perl commands for the program code.

Here's an example of writing a Perl script that runs on its own in the shell:

```
$ cat test2.pl
#!/usr/bin/perl
# This is another simple test Perl script
print "This is the second test script.\n";
$
```

Before you can run this Perl program, though, you must ensure that the Perl script file is set with execute permissions:

```
$ chmod +x test2.pl
$ ./test2
This is the second test script.
$
```

The chmod command changes the permissions for the owner of the file to run it from the shell. Now the Perl script can be run directly from the command-line prompt, or even from within shell scripts.

### Secret
Depending on how your PATH environment variable is set, you'll most likely need to use the ./ symbol before the script file name to tell the shell that the script file is located in the current folder. If you plan on running lots of Perl scripts from your current folder, you can add the dot symbol to the PATH environment variable in your shell session using the command:
$ PATH=$PATH:. ; export PATH
After running this command, you don't need to include the ./ portion when running your Perl scripts.

## Perl Programming

Just like any other programming language, Perl has specific rules for handling data, along with predefined operators and functions for acting on the data. This section describes the basic format of the Perl programming language. This should get you started in your Perl programming journey.
