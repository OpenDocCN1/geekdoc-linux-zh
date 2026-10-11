The double-headed arrows show how the input and output of the two types of pipes correspond to each other. All the details will be explained in subsequent sections, so you might want to refer to this figure as you proceed through the chapter. In the top part of the figure, the output of the `cat` command is transmitted through an unnamed pipe created in the kernel. Its output becomes `cut`'s input. This is a typical use of shell pipelines.

In particular, note that using named pipes requires that the order of the `cat` and `cut` commands is reversed. For reasons that will be explained later, the `cut` command must be executed first (and run in the background) so that you are able, in the same terminal or from the same console, to issue the `cat` command that provides the input to the named pipe.

The named pipe, `/tmp/myfifo`, and the unnamed pipe serve the same purpose, feeding their input to their output. All that really differs is the order in which commands are executed and the use of the shell redirection operators, > and <, when dealing with named pipes.

> **NOTE**
> Perhaps FIFOs are so named because they are also created using the `mkfifo` function!

Most Linux users are familiar with unnamed pipes, although they might not realize it. Every command such as the following uses unnamed pipes:

```
$ cat /etc/passwd | cut -f1 -d: | sort
```

In this example, the output from the `cat` command becomes the input to the `cut` command, whose output then becomes input to `sort`. As you know, the `|` is the pipe symbol. What you might not realize is that your shell probably implements `|` using the `pipe` function you will meet in a moment. Hopefully, it is clear that there is never an actual disk file associated with `|`.

> **CAUTION**
> A quick tip on terminology: Unless the distinction needs to be made clear, `pipe` in this chapter refers to unnamed pipes, and `FIFO` refers to named pipes. Both pipes and FIFOs, however, are `half duplex;` that is, data flows in only one direction, just as water in a drainage pipe flows in only one direction. Pipes and FIFOs are also `non-seekable;` that is, you can't use calls like `lseek` to position the file pointer.

Unnamed pipes have two shortcomings. First, as noted, they are half duplex, so data can travel in only one direction. Second, and more significantly, pipes can be used only between related processes, those that have a common ancestor. As you will recall from Chapter 4, "Processes," child processes created from a `fork` or an exec inherit their parent's file descriptors.

Figure 15.2 shows how data flows through a pipe.