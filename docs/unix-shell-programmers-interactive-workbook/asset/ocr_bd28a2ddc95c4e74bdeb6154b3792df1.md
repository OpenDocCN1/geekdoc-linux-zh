# Lab 2.2: Command Syntax

whence is a shell builtin
$

The whence command lets you find out the type of any command you give it. By default, whence doesn't say too much about the names of built-in commands, but you can use its -v option to make the output "verbose."

+   c) What happens if you don't use the -v option for these?
Answer:The output would be as follows:

$ whence builtin print whence
builtin
print
whence
$

That's not very interesting output, which is why you did it first with the -v option.

# 2.2.3 ANSWERS

Use ls /usr/bin to see a list of some external commands.

+   a) What are the results?
Answer:A long list of file names should appear.

The exact list depends on what system you are using. If you don't get a list, your system may use /bin instead of /usr/bin; try that instead.

Verify that you can run an external command by typing the full pathname of the executable file using /bin/ls.

+   a) What are the results?
Answer:A list of the files in the current directory should appear.