# 10
Getting a Handle
on Files

![](bbox=[0.55, 0.11, 0.87, 0.32])

Now it is time to see how Perl interacts with files, pipes, and command-line arguments. By the time you have finished this chapter, you should be able to explain the following script.

```
use feature 'say';
die "Insufficient arguments" if scalar @ARGV < 1;

while(<>){
    say "$ARGV $. $._";
    say "*" x 30 && close ARGV if eof;
}
```

# 10.1 The User-Defined Filehandle

If you are processing text, you will regularly be opening, closing, reading from, and writing to files. In Perl, we use filehandles to get access to system files.

A **filehandle** is a name for a file, device, pipe, or socket. In Chapter 4, "Getting a Handle on Printing," we discussed the three default filehandles, *STDIN*, *STDOUT*, and *STDERR*. Perl also allows you to create your own filehandles for input and output operations on files, devices, pipes, or sockets. A filehandle allows you to associate the filehandle name with a system file and to use that filehandle to access the file.

# 10.1.1 Opening Files—The open Function

The *open* function lets you name a filehandle and the file you want to attach to that handle. If the filehandle is an undefined scalar variable, a new file filehandle is created (called *autovivification*) as a reference to a new anonymous filehandle. If the filehandle is an expression, it is a symbolic reference to the named file. The file can be opened for reading, writing, or appending (or both reading and writing), and the file can be opened to pipe