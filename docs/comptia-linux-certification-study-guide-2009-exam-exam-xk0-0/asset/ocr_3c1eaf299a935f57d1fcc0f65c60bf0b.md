Of course, you probably aren't working on an old mainframe; processors are blazing fast and most bottlenecks now are hard drives and network interfaces, so niceness doesn't get adjusted very often. Chivraly may not be dead, but niceness is definitely fading.

# ## Leveraging I/O Redirection

One of the primary tenets of UNIX is the use of small programs that each do one thing very well.³ These small useful tools are meant to work together to build up the exact features needed to perform whatever task you need to perform. I/O redirection is the glue that sticks these handy little programs together.

Before digging in, it's important to understand that console programs make use of three *streams* for communicating. They are shown in Table 6.1.

When using a command line program, normally you provide input through the keyboard and the program responds with output and any problems it may encounter to the console. Things get interesting when you begin to harness the power of *redirection*. This allows you to use the output from one program as the input for another, or send it to a file. You can use the contents of a file as the input for a program, or use a succession of programs to create and manipulate information. It works like this:

```
$ some_program > someplace_other_than_the_console
```

To see what redirection looks like, check out Figure 6.11.

Although "someplace_other_than_the_console" is frequently a regular file, since Unix treats virtually everything as a file, it's just as easy to send the information to a printer port or other "file" – even the sound card, if you'll recall our previous experiment in the "Device Files" section.

> **Exam Warning**
> 
> Be careful when using >>; if you redirect your output stream to an existing file it will be overwritten. Use >> to append to the end of an existing file.

Table 6.1 The Three Communications Streams

| Name | Number | Symbol | Normal Connection |
| :--- | :--- | :--- | :--- |
| STDIN | 0 | < | Keyboard |
| STDOUT | 1 | > | Console (display) |
| STDERR | 2 | > | Console (display) |