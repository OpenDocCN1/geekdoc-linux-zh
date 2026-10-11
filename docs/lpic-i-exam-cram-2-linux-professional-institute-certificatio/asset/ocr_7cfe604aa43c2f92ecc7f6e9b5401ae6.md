# # Unix/Linux Toolset Mentality

In this chapter we focus on the concepts and practice of getting a lot done on the shell command line. Chief among the skills you will gain from this chapter is the ability to choose commands and chain them together properly, and sometimes interestingly, to get your work done.

Unix and Linux have a toolset mentality that needs to be cultivated, and it must be learned to be successful in your sysadmin/programming work and on the exams.

Everything in the Linux command arena needs to do three things:

+   - It should do one thing very well.
+   - It should accept standard input.
+   - It should produce standard output.

With these commands and the shell's constructs that help connect things together (pipes, redirection, and so on), it becomes possible to accomplish many things with just one command string of connected commands.

# ## Working with I/O Streams

Linux supports separate streams to handle data on the shell command line. These are called *file descriptors* and are used primarily to send data to and from programs and files and to handle errors.

The three file descriptors and their associated files are

| Name | fd Number | Associated File |
| :--- | :--- | :--- |
| */dev/stdin* | 0 | */proc/self/fd/0* |
| */dev/stdout* | 1 | */proc/self/fd/1* |
| */dev/stderr* | 2 | */proc/self/fd/2* |

Standard in, or *stdin*, is what all programs accept, or it's assumed they will accept. Most programs accept *stdin* either from a redirected file argument or using the file as an argument to the program:

```
program < file

or

program file
```