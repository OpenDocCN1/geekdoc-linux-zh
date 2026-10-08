
# Chapter 11: Using Command-Line Tools

wildcards can be extremely hard when working with directories containing multiple files with similar names. Consider the following directory containing several files in different formats:

```
$ ls
dlt01.flac dlt04.flac dlt07.flac dlt10.flac d202.flac
dlt01.mp3 dlt04.mp3 dlt07.mp3 dlt10.mp3 d202.mp3
dlt01.wav dlt04.wav dlt07.wav dlt10.wav d202.wav
dlt02.flac dlt05.flac dlt08.flac dlt11.flac d203.flac
dlt02.mp3 dlt05.mp3 dlt08.mp3 dlt11.mp3 d203.mp3
dlt02.wav dlt05.wav dlt08.wav dlt11.wav d203.wav
dlt03.flac dlt06.flac dlt09.flac d201.flac Horslips info.txt
dlt03.mp3 dlt06.mp3 dlt09.mp3 d201.mp3 playlist.m3u
dlt03.wav dlt06.wav dlt09.wav d201.wav
```

You'll note that these filenames follow a certain convention, in which this case is <number>.format. To list the MP3 files in this directory that are the first track on a given disk, you could use the following:

```
$ ls d201.mp3
dlt01.mp3 d201.mp3
```

This uses the question mark to represent the disk number, which is a single digit in my sample filenames.

Similarly, to list all the MP3 files in this directory, you could use the asterisk as matching filename with the .mp3 file extension, in the following example:

```
$ ls *.mp3
dlt01.mp3 dlt04.mp3 dlt07.mp3 dlt10.mp3 d202.mp3
dlt02.mp3 dlt05.mp3 dlt08.mp3 dlt11.mp3 d203.mp3
dlt03.mp3 dlt06.mp3 dlt09.mp3 d201.mp3
```

Assume that you want to list just the files with extensions that are either flac or wav. You could do this using the curly wildcard in the command:

```
$ ls *.flac
dlt01.flac dlt04.flac dlt07.flac dlt10.flac d202.flac
dlt01.wav dlt04.wav dlt07.wav dlt10.wav d202.wav
dlt02.flac dlt05.flac dlt08.flac dlt11.flac d203.flac
dlt02.wav dlt05.wav dlt08.wav dlt11.wav d203.wav
dlt03.flac dlt06.flac dlt09.flac d201.flac
dlt03.wav dlt06.wav dlt09.wav d201.wav
```

Finally, suppose you want to list all the seventh and eighth songs in MP3 format from the first disk in your directory. You could do this using the square bracket wildcard, as in the following:

```
$ ls dlt0[78].mp3
dlt07.mp3 dlt08.mp3
```

# Part II: Ubuntu for Desktop Users

You can combine any of these wildcards to identify increasingly specific sets of files. For example, the following would identify just the seventh and eighth songs from the first disk that are in flac and wav format:

```
$ ls dlt0[78].*(flac.wav)
dlt07.flac dlt07.wav dlt08.flac dlt08.wav
```

The shell provides a very powerful wildcard mechanism. Wildcards such as these are especially useful when you want to move, copy, or delete groups of files.

# Tip

If you're familiar with wildcards on other types of systems, be careful: Linux wildcards may not work exactly the same way. For example, on some systems, you can type something like ren *.foo to rename files with the .txt extension to the same base filename but the .foo extension. This will not work on a Linux system because wildcards are expanded before the command is executed. The *.foo portion of the command line will not match anything but for files with that extension currently.

# Pipes and Input and Output Re-Direction

As discussed in Chapter 1, "The Ubuntu Linux Project," a core element of the basic philosophy of UNIX, therefore Linux is that utilities should do one thing and do it well. This alleviates the need for a lot of duplicate code by enabling one command to process the output produced by another. For example, you might want to find the number of files in a directory by listing the files in a directory, and then counting the number of files. One way to do this is to write the output of the ls command to a temporary file, and then count the number of lines in that temporary file using the Linux wc -l command. Linux makes it easy to write the output of a command to a file by what is called output re-direction, which is represented on the command line by the greater-than symbol (>). As an example, the following command writes the output of the ls command to the temporary file /tmp/my_dir_list.txt:

```
$ ls > /tmp/my_dir_list.txt
```

I could count the number of lines in that file using the wc -l command, as in the following example:

```
$ wc -l /tmp/my_dir_list.txt
8
```

There are apparently eight files in my current directory. However, using a temporary file requires some extra typing and also requires that you clean up after yourself. Luckily, Linux comes to the rescue again with the notion of using a special symbol, the vertical bar, to connect the output of one command to the input of another. This symbol (|) is known as a pipe. You could use a pipe to avoid the temporary file and get the same results by typing a command such as following:

```
$ ls | wc -l
8
```

# Chapter 11: Using Command-Line Tools

If you find yourself performing many command-line operations, you will find both the output re-direction and pipe concepts to very convenient. Re-directing output is an easy way of keeping track of the contents of files and directories, recording system information, and so on.

An more interesting use of output re-direction is its ability to append some amount to an existing file. In the previous example, using a single greater-than symbol creates a file if it doesn't exist, but overwrites the contents of that file if it already exists. You may want to append to an existing file rather than completely overwrite it, which you can easily do by using two greater-than signs rather than a single one, as in the following example:

```
$ ls /tmp/my_dir_list.txt
$ ls >> /tmp/my_dir_list.txt
$ wc -l /tmp/my_dir_list.txt
16
```

As you can see, the temporary file now contains twice as many lines, which is what you'd expect because

The bash shell supports input-direction, which is the ability to read data from a file as input to another command. For complete information on input-direction and re-direction, in general, see the online help for the bash shell.

# Introducing Job Control

$ emacs myfile.txt &
[1] 7539

Starting a command in the background is known in Linux and causes the shell to display two bits of information:

- The job number (inside brackets)
- The process ID of the process that was

The job number is useful because it is possible to run multiple commands in the background at the same time. The job number therefore provides a unique way of identifying any background command. The job number is an identifier for that background job within the context of your current shell. The process identifier is a unique identifier for that process in terms of your entire system.

# Tip

If you forget the ampersand while trying to start a command in the background, you can always suspend the command using the Ctrl-z key combination, and the bg (background) command to start it in the background.

Why care identifying these processes? Primarily so that you can terminate them or bring them to the foreground. For example, suppose that you accidentally started started a command in the background, but that command actually requires interactive input. To bring a background command back to the foreground (meaning that it is interactively running in the current shell), you can simply refer to it using a percent symbol and its job number, as in the following example:

```
$ %1
```

This would bring the emacs command back to the foreground so that anything you type in the shell is actively sent to the command. Suppose, however, you've lost your Linux window on the screen and simply want to terminate the background job manually. You can do this by using the Linux kill command, providing the job number to identify the job you want to terminate, as in the following example:

```
$ kill %1
```

Knowing not only the job number for a background process but its system-wide process identifier enables you to use the kill command to terminate a process from another shell. Because job numbers are unique to a specific shell, you can use the kill command to terminate a process-by-process ID from any shell or terminal session, as in the following example:

```
$ kill 7539
```

Being able to execute long-running commands in the background is very important in today's multi-windowed graphical environments because you usually want to be able to continue your current shell while the long-running command continues on its merry way.

As always, job control is much more flexible and powerful than the introduction given here. For complete information on job control, use the info command to see the online reference information for the bash shell.
