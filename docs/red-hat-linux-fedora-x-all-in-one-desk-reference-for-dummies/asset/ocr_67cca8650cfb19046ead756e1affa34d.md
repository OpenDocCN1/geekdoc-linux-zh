# Becoming root for the GUI Utilities 395

That's a long list of tasks! I don't cover all of them in this chapter, but the rest of the minibook describes most of these tasks. Here I focus on some of the basics, such as how to become root (the superuser), setting system-configuration files, monitoring system performance, and setting up periodic jobs.

# How to Become root

You have to log in as root to perform the system administration tasks. The root user is the superuser and the only account with the privileges needed to do anything in the system.

Common wisdom says you should not normally log in root. When you're root, one mistake and you can easily delete all the files — especially when typing commands. Take, for example, the command rm *.html that may type to delete all files that have the .html extension. If you accidentally press the space after the asterisk (*)? The shell tells you the command to be rm *.html and — because * causes any filename deletes everything in the current directory. Seems implausible until it happens to you!

# Using the su - command

If you're logged in as a normal user, how do you do any administration changes? Well, you become root for the time being. If you're working at a terminal window or console, type

```
su
```

Enter the root password in response to the prompt. From this point, you're root. Do whatever you have to do. To return to your usual self, type

```
exit
```

That's it! It's easy.

# Becoming root for the GUI Utilities

If you use Fedora Core's GUI utilities to perform a system administration change, it's even easier. Typically, the utility pops up a dialog box that prompts you for the root password (as in Figure 1-1). Just type the word and press Enter. If you don't want to use the utility, click Close.

| Book Chapter 1 | Administration Performing Basic |