# Laying pipes

Another *bash* shell feature enables you to connect commands so that the output of one becomes the input for the next one. This feature is referred to as a *pipe*. Suppose that you want to look over the details of all files in the /etc directory in long-listing format. If you type `ls -la /etc` to do so, a massive listing appears, and much of the information scrolls right past you. Although you can back up a bit by pressing Shift-PageUp, you may not be able to see everything.

To see all the information, you can do one of two things:

+   » Send the data to a file with redirection by typing something like `ls -la /etc > ~/etclisting` and then review the contents of ~/etclisting with your favorite editor.
+   » Pipe the output to the *more* command (see Appendix A).

To pipe the output to *more*, type `ls -la directory_path | more`, where *directory_path* is the directory for which you want to list the contents. The | symbol (which on the keyboard looks more like two vertical bars stacked on top of each other rather than just one solid line) tells *bash* that you want to use a pipe. The output from the *ls* command is sent "behind the scenes" to the *more* command, which then is responsible for displaying it on the monitor in pages.

# “Help!”

The *man page* system is the electronic manual for *Linux* (*man* is short for *manual*), designed to provide users with a convenient reference to all the detailed command information. This information includes command-prompt options, file formats, and program function usage.

The syntax for opening a *man page* is *man <command name>*.

Don't know the command you're looking for or need basic information about using the *man page* system? Just type *man man* to get started. When you're finished reading the *man* page, press Q to exit.

# Clearing the screen

The *clear* and *reset* commands are handy to know about when you're working in a shell. The *clear* command simply wipes the *bash* screen clean. Don't worry; it's not deleting any files, clearing out the command history, or changing any