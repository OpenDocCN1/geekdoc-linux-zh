# Chapter 2

# Scripting and the Shell

+   - Comment at the level you yourself will find helpful when you return to the script after a month or two. Some useful points to comment on are the following: choices of algorithm, reasons for not doing things in a more obvious way, unusual paths through the code, anything that was a stumbling block during development. Don't clutter code with useless comments; assume intelligence and language proficiency on the part of the reader.
- Code work best at the granularity of blocks or functions. Comments that describe the function of a variable should appear with the variable's declaration or first use.
- It's OK to run scripts as root, but avoid making them setuid; it secure. Use sudo to implement appropriate access control policies instead.
- With bash, -x to echo commands before they are executed and -n to check commands for syntax without executing them.
- Perl's -w option warns about suspicious behaviors as variables used before their values are set. You can include this on a script's shebang line or turn it on in the program's text with warnings.
- In Python, you are in debug mode unless you turn it off with a -0 argument on the command line. That means you can test the _debug_ variable before printing diagnostic output.

Tom Christensen suggests the following five Golden Rules for producing useful error messages:
- Error messages should go to STDERR, not STDOUT.
- Include the name of the program that is issuing the error.
- State what function or operation failed.
- If a system call fails, include the perror string ($! in Perl).
- Exit with some error code other than 0.

Perl makes it easy to follow all five rules:
die "can't open $filename:"

# 2.7 RECOMMENDED READING

BROOK, FREDERICK P, JR. The Mythical Man-Month: Essays on Software Engineering. Reading, MA: Addison-Wesley, 1995.

# Shell basics and bash scripting

ALBING, CARL, JP VOSSEN, and CAMERON NEWHAM. Bash Cookbook. Sebastastopol, CA: O'Reilly Media, 2007.