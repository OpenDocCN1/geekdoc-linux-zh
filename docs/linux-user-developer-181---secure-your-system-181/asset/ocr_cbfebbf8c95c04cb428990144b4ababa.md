new directories is **mkdir**. Type `mkdir sandbox` and press **Enter**; this will create a new directory called `sandbox`.

Once this directory is created, we will want to move into it. Use the **cd** command to change directory. If we want to move into our new `sandbox` directory, we type:

```
$ cd sandbox
```

If you type `pwd` and press **Enter** again, you will see that you are now inside the `sandbox` directory.

We refer to `mkdir` as a "command", but it is actually a program in its own right. Indeed, the basic mode of operation for the terminal is: when the user types the name of a program, run that program. Programs can take in arguments on the command line (for example, the `sandbox` in `mkdir sandbox`, which affect their behaviour.

As we will see later, these programs can be combined together to make a powerful language in which the programs take on the role of commands. We can use this language to write scripts to automate repetitive tasks.

Our new directory is currently empty. Indeed, if we now type **ls** at the command line and press **Enter**, we get no output. In order to illustrate various commands, let's create some files in the directory. We'll use the `touch` command to create some empty files:

```
$ touch email01.txt email02.txt email03.txt
$ touch work01.txt work02.txt work03.txt
$ ls
email01.txt email02.txt email03.txt
work01.txt work02.txt work03.txt
```

If we want to, we can delete files with the `rm` command: type `rm work03.txt` to delete that file.

The files created by `touch` are empty. If we want files with some content to them, we'll need to use different tools. If you like, you can use a text editor to create your own files to experiment with, but in this tutorial we shall get a text file from the internet using the `wget` command.

There is a chance that wget is not installed on your system. Try typing wget at the command line: if you get a 'command not found' error, then you will need to install it using your distro's package manager.

# ## Combining commands

Once you have wget installed, type `wget https://www.gutenberg.org/files/2701/old/moby10b.txt` and press **Enter**. This will download the text of the novel Moby Dick from an online public-domain repository. You can use the same command to download any file on the world wide web. You might like to type **ls** again, to make sure that this text file is now in your working directory alongside the other files we just created using `touch`.

If we want to delete a directory, we can use the `rm` command. Note, however, that this only works for directories that are empty:

```
$ mkdir new
$ touch new/file.txt
$ rmdir new
```

![](bbox=[0.43, 0.15, 0.85, 0.35])

Above The terminal emulators available for Linux come in all sorts of sizes and colours. You might have more than one installed on your system

```
$ rmdir: failed to remove 'new': Directory not empty
```

In order to delete a directory that contains files, we can use `rm -rf`. For example:

```
$ rm -rf new
$ ls
email01.txt email02.txt email03.txt
moby10b.txt work01.txt work02.txt
```

This is a new way to use the rm program. The `-rf` part is called a "switch" or a "command-line option" and it causes `rm` to act in a different but related way. Whenever you see one or two dashes followed by one or more letters

> "The true power of the command line becomes apparent when we combine two or more commands together"

in a Linux command, you are looking at a command-line switch. `-rf` contains two letters, which are actually two separate command-line switches: r tells the program to remove a directory and all the files in it recursively, while f is short for "force". If you miss out the f and write `rm -r`, new, then rm will sometimes prompt you to ask if you really want to delete those files. If you trust yourself not to delete the wrong thing accidentally, you can save yourself a bit of time by using rm -rf.

Most Linux commands have switches that can change their behaviour. For example, `echo` -- print the phrase without starting a new line at the end. So far, we have seen examples of individual commands, but the true

# ## UNIX is an IDE

One school of thought holds that "UNIX is an IDE". The idea is that, by running commands in one or more terminals, you can replicate the same functionality that you might see in a more advanced IDE such as Eclipse. You can run editors such as nano and vi in the terminal, as well as program-ming tools such as gdb and debuggers. If you throw in a few shell scripts to tie things together, you can program efficiently without leaving the terminal.