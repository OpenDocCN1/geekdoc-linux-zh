You can see in this example that the response I typed of "MANY DIFFERENT PLACES" was indeed read into *REPLY*.

Although **echo** is used throughout this chapter, you may also see **print** used display lines on the screen.

# Arguments to Shell Programs

Shell programs can have command-line arguments just like any regular command. Command-line arguments that you use when you invoke your shell program are stored in a special set of variables. These are called the positional parameters.

The first ten words on the command line are directly accessible in the shell program using the special variables **$0-$9**. This is how they work:

+   $0	The command name
$1	The first argument
$2	The second argument
$3	.
	.
	.
$9	The ninth argument

If you are not sure how many command line arguments you may get when your program is run, there are two other variables that can help:

+   $#	The number of command-line arguments
$*	A space-separated list all of the command-line arguments (which does not include the command name)