+   - ssh—Connects to other machines
+   - tail—Prints the last lines of a file
+   - top—Prints resource usage
+   - vim—A text editor
+   - which—Prints the location of a command
+   - xargs—Executes commands from its input

Of course, many other commands are available to you that get used fairly often—diff, nmap, ping, su, uptime, who, and so on—but if you are able to understand the 25 listed here, you will have sufficient skill to concoct your own command combinations.

Note that we say understand the commands—not know all their possible parameters and usages. This is because several of the commands, though commonly used, are used only in any complex manner by people with specific needs. gcc and make are good examples of this: Unless you plan to become a programmer, you need not worry about these beyond just typing make and make install now and then. If you want to learn more about these two, see Chapter 30, "C/C++ Programming Tools for Ubuntu."

Similarly, both Emacs and Vim are text editors that have a text-based interface all of their own, and SSH has already been covered in detail in Chapter 19, "Remote Access with SSH and Telnet."

What remains is 20 commands, each of which has many parameters to customize what it actually does. Again, we can eliminate much of this because many of the parameters are esoteric and rarely used, and the few times in your Linux life that you need them, you can just read the manual page!

We will be going over these commands one by one, explaining the most common ways to use them. There is one exception to this: The xargs command requires you to understand how to join commands together.

Most of these commands have been touched on elsewhere in the book, primarily in the "Using the Shell" section of Chapter 5, "First Steps with Ubuntu." The goal of that section was to give you "the least you need to know" to get by, whereas in this chapter each command is treated individually with an aim to giving you the confidence needed to be able to mix them together to create your own commands.

# Printing the Contents of a File with cat

Many of Ubuntu's shell commands manipulate text strings, so if you want to be able to feed them the contents of files, you need to be able to output those files as text. Enter the cat command, which prints the contents of any files you pass to it.