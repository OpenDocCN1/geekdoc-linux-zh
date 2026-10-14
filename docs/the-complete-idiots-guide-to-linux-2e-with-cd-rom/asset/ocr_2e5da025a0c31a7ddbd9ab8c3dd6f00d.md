To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

# STDERR

The standard error stream, or STDERR, is where error messages are sent. As you enter more complex commands on a shell, you'll probably want to have diagnostic or warning messages sent to a log file. Redirecting error messages to a new file is especially useful if you are debugging a shell script.

# Redirecting Errors

By default, both STDERR and STDOUT point to your console so you can see diagnostic messages. When you redirect STDOUT, STDERR still points to your console, and any errors are still printed there. To redirect errors, you need to specify a file number.

The input, output, and error streams have assigned file numbers in the shell: STDOUT is 0, STDIN is 1, and STDERR is 2. You can combine the file number and the redirection operator. To redirect errors to a different place, you specify the redirection like this:

```
command > outputfile 2> errorfile
```

Messages printed to the standard error stream, STDERR, will go to errorfile, and standard output to STDOUT will redirect outputfile.

For example, let's say you wanted to create a list of all the files on your system. Depending on your user id, you might not have permission to go into some directories. The following command line will redirect permission access errors to a different file while capturing good output in a separate file: