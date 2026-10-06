# Chapter 15 The Z Shell and Advanced Shell Programming

file with the file. Each process has its own set of open files and its
descriptors. After opening a file, a process reads from and writes to that file by
referring to it the file descriptor. When it no longer needs the file, the process
closes the file, freeing the file descriptor.

A typical GNU/Linux process starts with three open files: standard input (file
descriptor 0), standard output (file descriptor 1), and standard error (file descriptor-
tor 2). Often others are all the files process needs. The Z Shell allows you to re-
direct input, standard output, and standard error of all the commands you
incline, just as the Bourne Again Shell does. Recall that you can redirect-
output with the symbol > or the symbol 1 and that you redirect standard-
row with the symbol 2>. You can redirect other file descriptors, because file
descriptors other than 0, 1, and 2 do not have any special meaning,
it's rarely useful to do so. The exception is in programs that you write yourself,
which case you control the meaning of the file descriptors and can take advantage
redirection.

The Bourne Again and Z Shells open files using the exec builtin as:

```
zsh % exec 3> outfile
zsh % exec 4< outfile
```

The first command opens for output and holds it open, associating it with
file descriptor 3. The second command opens file for input, associating it with file
descriptor 4.

The token <& duplicates both input and output file descriptors. You can dupli-\cate file descriptor by making it refer to the same file as another open file descrip-
tor, as standard input or output. The following command opens or redirects
file descriptor n as a duplicate of file descriptor m:

```
zsh % exec n&>m
```

Once you have opened a file, you can use it for input and output in two differ-\ents. First, you can use I/O redirection on any command line, redirecting stan-\dard to a file descriptor with>&n or redirecting standard input from a file
descriptor with<& Second, you can use the read (page 775) and print (page 778)
buildins. When you invoke other commands, including functions (pages 672 and 784),
t inherit these open files and file descriptors. When you have finished using
file, you can close it with

```
exec n<&-
```

When you invoke the next shell function with two arguments, it copies the file
named by the first argument to the file named by the second argument: mycp
src to dest. If you supply only one argument, the script interprets it as a source and
copies src to standard output. If you invoke mycp with no arguments, it copies stan-
 input to standard output: