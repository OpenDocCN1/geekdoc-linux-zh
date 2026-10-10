+   ➤ ssh—Connects to other machines
+   
+   ➤ tail—Prints the last lines of a file
+   
+   ➤ top—Prints resource use
+   
+   ➤ vim—A text editor
+   
+   ➤ which—Prints the location of a command
+   
+   ➤ xargs—Executes commands from its input

Of course, many other commands are available to you and are used fairly often—diff, man, ping, su, uptime, who, and so on—but if you are able to understand the 25 listed here, you will have sufficient skill to concoct your own command combinations.

Note that we say understand the commands—not know all their possible parameters and uses. This is because several of the commands, although commonly used, are used only by people with specific needs. gcc and make are good examples of this: Unless you plan to become a programmer, you need not worry about these beyond just typing make and make install now and then. If you want to learn more about these two commands, refer to Chapter 28, “C/C++ Programming Tools for Fedora.”

Similarly, both Emacs and Vim are text editors that have a text-based interface all their own, and SSH has already been covered in detail in Chapter 15, “Remote Access with SSH.”

What remains are 20 commands, each of which has many parameters to customize what it actually does. Again, you can eliminate many of these because many of the parameters are esoteric and rarely used, and, the few times in your Linux life that you need them, you can just read the manual page!

We go over these commands one by one, explaining the most common ways to use them. There is one exception to this: The xargs command requires you to understand how to join commands together, so it is bundled in the section “Combining Commands.”

Most of these commands have been touched on elsewhere in the book, primarily in Chapter 4, “Command-Line Quick Start.” The goal of that chapter was to give you “the least you need to know” to get by, whereas in this chapter each command is treated individually with an aim to giving you the confidence needed to be able to mix them together to create your own commands.

# Printing the Contents of a File with cat

Many of Fedora’s shell commands manipulate text strings, so if you want to be able to feed them the contents of files, you need to be able to output those files as text. Enter the cat command, which prints the contents of any files you pass to it. Its most basic use is like this:

```
$ cat myfile.txt
```