# Redirection

Before we cover viewing files, let’s talk about redirection for a minute because I use some redirection in the upcoming section. I cover redirection under shell programming, but for now I want to give you just a quick introduction to redirection so that we can more effectively cover some of the commands in this chapter.

UNIX is set up such that commands usually take their input from the keyboard, often called *standard input*, and usually send output to the screen, often called *standard output*. Commands also send error information to the screen. It is not always desirable for input to come from standard input and output and errors to go to standard output. You are given a lot of control to override these defaults. This is called redirection. Table 10-1 shows many common forms of redirection.

As shown in the table, to redirect the output of a command from standard output to a file, you would use ">". This works almost all of the time. If you have an environment variable called **noclobber** set, then redirecting to an existing file does not work (we’ll cover environment variables shortly). The **noclobber** does not permit redirection to write over an existing file. If you try to write over an existing file, such as /tmp/processes below, you receive a message that the file exists:

![](bbox=[0.05, 0.68, 0.15, 0.74])

```
# ps -ef > /tmp/processes
/tmp/processes: File exists
```

You can, however, use "!" with redirection to force a file to be overwritten. Using ">!" forces a file to be overwritten, and ">>!" will force the output to be appended to the end of an existing file. Examples of these are shown in Table 10-1.