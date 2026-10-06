# Using numbers with commands

You can precede vi commands with numbers to have the command repeated that number of times. This is a handy way to deal with several lines, words, or characters at a time. Here are some examples:

+   - 3dw Deletes the next three words.
- 5cl Changes the next five letters (that is, removes the letters and enters input mode).
- 12j Moves down 12 lines.

Putting a number in front of most commands just repeats those commands. At this point, you should be fairly proficient using the vi command. If you would like further instruction, I suggest you the VI Tutor by using the vimutor

> NOTE: When you invoke vi on Fedora or RHEL, you're actually invoking vi text editor, which runs vi compatibility mode. Those who do a lot of programming might prefer vim, because it shows different levels of code in different colors. vim has other useful features, such as the ability to open a document with the cursor at the same place where it was when you last exited that file.

# Summary

Working from a shell command-line interpreter within Linux may not be as simple as using a GUI, but it offers many powerful and flexible features. This chapter describes how to log in to Fedora or RHEL and use shell commands. Features for running commands include recalling commands from a history list, completing commands, and joining commands.

This chapter describes how shell environment variables can be used to store and recall important pieces of information. It also teaches you to modify shell configuration files to tailor the shell to suit your needs. Finally, this chapter describes how to use the Linux file system to create files and directories, set permissions, and work with files (moving, copying, and removing them), and to edit text files from the shell using the vi command.