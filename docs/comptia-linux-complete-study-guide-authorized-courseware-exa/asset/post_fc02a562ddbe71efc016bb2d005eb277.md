
# **EXERCISE 1.1** _(continued)_

- 5. Type `1s -l t`, and without pressing the Enter key, press the Tab key. The system may beep at you or display two `three`. If it doesn't display two `three`, press the Tab key again, and it should do so. This reveals that either two or three is a valid completion to your command, because these are the two files in the test directory whose file-names begin with the letter `t`.
- 6. Type `h`, and again without pressing the Enter key, press the Tab key. The system should complete the command `1s -l three`, at which point you can press the Enter key to execute it. (You'll see information on the file.)
- 7. Press the Up arrow key. You should see the `1s -l three` command appear on the command line.
- 8. Press Ctrl+A to move the cursor to the beginning of the line.
- 9. Press the Right arrow key once, and type `es` (without pressing the Enter key). The command line should now read `less -l three`.
- 10. Press the Right arrow key once, and press the Delete key three times. The command should now read `less` `three`. Press the Enter key to execute the command. (Note that you can do so even though the cursor isn't at the end of the line.) This invokes the `less` pager on the `three` file. (The `less` pager is described more fully later, in “Getting Help.”) Because this file is empty, you'll see a mostly empty screen.
- 11. Press the Q key to exit from the `less` pager.

## Exploring Shell Configuration

Shells, like many Linux programs, are configured through files that hold configuration options in a plain-text format. The bash configuration files are actually bash shell scripts, which are described more fully in Chapter 9. For now, you should know that the `~/.bashrc` and `~/profile` files are the main user configuration files for bash, and `/etc/bash.bashrc` and `/etc/profile` are the main global configuration files.

Even without knowing much about shell scripting, you can make simple changes to these files. Edit them in your favorite text editor, and change whatever needs changing. For instance, you can add directories to the $PATH environment variable, which takes a colon-delimited list of directories.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_71_0.png)

> Be careful when changing your bash configuration, and particularly the global bash configuration files. Save a backup of the original file before making changes, and test your changes immediately by logging in using another virtual terminal. If you spot a problem, revert to your saved copy until you can learn the cause and create a working file.

## Using Environment Variables

Environment variables are like variables in programming languages—they hold data to be referred to by the variable name. Environment variables differ in that they're part of the environment of a program, and other programs, such as the shell, can modify this environment. Programs can rely on environment variables to set information that can apply to many different programs. For instance, suppose a computer hosts several different Usenet news readers. These programs all need to know what Usenet news server to use; if they all agree to use an environment variable, such as $NTPSERVER, to hold this information, you can set this environment variable once as part of your shell startup script and then forget it. You needn't set this feature individually for all the news readers installed on the system.

Chapter 9 describes environment variables and their manipulation in more detail. For the moment, you should know that you can set them in bash by using an assignment (=) operator followed by the `export` command:

```
$ NTPSERVER=news.abigisp.com
$ export NTPSERVER
```

You can combine these two commands into a single form:

```
$ export NTPSERVER=news.abigisp.com
```

Either method sets the $NTPSERVER environment variable to news.abigisp.com. (When setting an environment variable, you omit the dollar sign, but subsequent references include a dollar sign to identify the environment variable as such.) Hereafter, programs that need this information can refer to the environment variable. In fact, you can do so from the shell yourself, using the `echo` command:

```
$ echo $NTPSERVER
news.abigisp.com
```

You can also view the entire environment by typing `env`. The result is likely to be several dozen lines of environment variables and their values. Chapter 9 describes what many of these variables are in more detail.

To delete an environment variable, use the `unset` command, which takes the name of an environment variable (without the leading $ symbol) as an option. For instance, `unset NTPSERVER` removes the $NTPSERVER environment variable.

# Getting Help

Linux provides a text-based help system known as `man`. This command’s name is short for *manual*, and its entries (its `man` pages) provide succinct summaries of what a command, file, or other feature does. For instance, to learn about `man` itself, you can type `man man`. The result is a *description* of the `man` command.

The `man` utility uses the `less` pager to display information. This program displays text a page at a time. Press the spacebar to move forward a page, Esc followed by V to move back a page, the arrow keys to move up or down a line at a time, the slash ( / ) key to search for text, and so on. (Type `man less` to learn all the details, or consult the upcoming section “Paging Through Files with `less`.”) When you’re done, press Q to exit `less` and the `man` page it’s displaying.

Linux `man` pages are categorized into several sections, which are summarized in Table 1.1. Sometimes a single keyword has entries in multiple sections; for instance, `passwd` has entries under both section 1 and section 5. In most cases, `man` returns the entry in the lowest-numbered section; but you can force the issue by preceding the keyword by the section number. For instance, typing `man 5 passwd` returns information on the `passwd` file format rather than the `passwd` command.

TABLE 1.1 Manual Sections

| Section Number | Description |
| :--- | :--- |
| 1 | Executable programs and shell commands |
| 2 | System calls provided by the kernel |
| 3 | Library calls provided by program libraries |
| 4 | Device files (usually stored in /dev) |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous (macro packages, conventions, and so on) |
| 8 | System administration commands (programs run mostly or exclusively by root) |
| 9 | Kernel routines |

Some programs have moved away from `man` pages to `info` pages. The basic purpose of `info` pages is the same as that for `man` pages, but `info` pages use a hypertext format so that you can move from section to section of the documentation for a program. Type `info info` to learn more about this system.

Both man pages and info pages are usually written in a terse style. They're intended as reference tools, not tutorials; they frequently assume basic familiarity with the command, or at least with Linux generally. For more tutorial information, you must look elsewhere, such as this book or the Web. The Linux Documentation Project (http://tldp.org) is a particularly relevant Web-based resource for learning about various Linux topics.

# Using Streams, Redirection, and Pipes

Streams, redirection, and pipes are some of the more powerful command-line tools in Linux. Linux treats the input to and output from programs as a stream, which is a data entity that can be manipulated. Ordinarily, input comes from the keyboard and output goes to the screen (which in this context can mean a full-screen text-mode login session, an xterm or a similar window, or the screen of a remote computer via a remote login session). You can redirect these input and output streams to come from or go to other sources, though, such as files. Similarly, you can pipe the output of one program into another program. These facilities can be great tools to tie together multiple programs.

> Part of the Unix philosophy to which Linux adheres is, whenever possible, to do complex things by combining multiple simple tools. Redirection and pipes help in this task by enabling simple programs to be combined together in chains, each link feeding off the output of the preceding link.

## Exploring Types of Streams

To begin understanding redirection and pipes, you must first understand the different types of input and output streams. Three are most important for this topic:

- **Standard input** Programs accept keyboard input via *standard input*, or stdin. In most cases, this is the data that comes into the computer from a keyboard.

- **Standard output** Text-mode programs send most data to their users via *standard output* (a.k.a. stdout), which is normally displayed on the screen, either in a full-screen text-mode session or in a GUI window such as an xterm. (Fully GUI programs such as GUI word processors don't use standard output for their regular interactions, although they might use standard output to display messages in the xterm from which they were launched. GUI output isn't handled via an output stream in the sense I'm describing here.)

- **Standard error** Linux provides a second type of output stream, known as *standard error*, or stderr. This output stream is intended to carry high-priority information such as error messages. Ordinarily, standard error is sent to the same output device as standard output,
