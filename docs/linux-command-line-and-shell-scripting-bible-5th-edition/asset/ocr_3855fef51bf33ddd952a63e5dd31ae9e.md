# Part I: The Linux Command Line

The *substitute* command, performed within Ex mode, allows you to quickly replace (substitute) one word for another in the text. To get to the substitute command, you must be in command mode. The format for the substitute command is *`:s/old/new/`*. The vim editor jumps to the first occurrence of the text (*`old`* in this case) and replaces it with the new text (shown here as *`new`*).

You can make a few modifications to the substitute command to replace more than one occurrence of the text:

+   - *`:s/old/new/g`* replaces all occurrences of *`old`* in a line.
+   - *`:n,ms/old/new/g`* replaces all occurrences of *`old`* between line numbers *`n`* and *`m`*.
+   - *`:\$s/old/new/g`* replaces all occurrences of *`old`* in the entire file.
+   - *`:\$s/old/new/gc`* replaces all occurrences of *`old`* in the entire file, but prompts for each occurrence.

As you can see, for a console mode text editor, vim contains quite a few advanced features. Because nearly every Linux distribution includes it, it's a good idea to at least know the basics of the vim editor so that you can always edit scripts, no matter where you are or what you have available.

# Navigating the nano Editor

In contrast to vim, which is a complicated editor with powerful features, *nano* is a simple editor. For individuals who need a simple console mode text editor that is easy to navigate, *nano* is the tool to use. It's also a great text editor for those who are just starting on their Linux command-line adventure.

The nano text editor is a clone of the UNIX systems' Pico editor. Although Pico also is a light and simple text editor, it is not licensed under the GPL. Not only is the nano text editor licensed under the GPL, it is also part of the GNU project.

The nano text editor is installed on most Linux distributions by default. Everything about the nano text editor is easy. To open a file at the command line with nano, enter

```
```bash
$ nano myprog.c
```
```

If you start nano without a filename or if the file doesn't exist, nano simply opens a new buffer area for editing. If you specify an existing file on the command line, nano loads the entire contents of the file into a buffer area, where it is ready for editing, as shown in Figure 10.2.

Notice at the bottom of the nano editor window, there are various commands with brief descriptions. These commands are the nano control commands. The caret (*`^`*) symbol represents the Ctrl key. Therefore, *`^X`* stands for the keyboard sequence Ctrl+X.

> **TIP**
> Though the nano control commands list capital letters in the keyboard sequences, you can use lowercase or uppercase characters for control commands.