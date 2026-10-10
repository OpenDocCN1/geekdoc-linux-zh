The options I’ve chosen to list are by no means comprehensive. These commands can be very powerful, and you should use them with care. If you’re uncertain of how to use a command or what a command does, simply type in man [command] to find a summary of the command’s properties. (There are some commands that do not have man pages, however.) Remember that you usually cannot severely damage the system unless you’re logged in as root (or using the super user via the su command), so experiment a little bit. At worst, you’ll simply have to back up the data files in your account and re-create it.

One of the most useful commands you’ll find is man. Anytime you’re using the command line and don’t know what a command does or what options it takes, you can use the man command to find out. If you’re not sure what the exact command is but know what it can do, use the apropos command to find out which man pages the keyword falls on.

# Piping

Piping is a term we use to describe redirecting program output. What this means is that you take the output from one program and use it as the input for another. A superfluous example is found in the command cat mylog.txt | more. (This is superfluous because using more mylog.txt will do exactly the same thing.) The concatenate command will not break the text stream page by page, but the more command will; so we take the output of cat and pipe it into more. This produces the same result as if we had simply used the more command by itself.

The | symbol is what is known as a pipe. (Hence the term piping.) There are other piping symbols as well. Here is a brief summary:

+   - `<[filename]` This pipe will take the contents of filename and use them as the input. This is especially useful in situations in which you want to debug a program.
+   - `> [filename]` This pipe takes the output of a program and places it in a file; if the file already exists, this will overwrite the file.
+   - `>> [filename]` This pipe does the same thing as the last, but instead of overwriting a file if it already exists, it appends to it.
+   - `| [command]` As we discussed above, this pipe takes the output from one command and uses it as the input for another.