For the first half of this book, you tied together everything that had been presented, rather neatly, by looking at the V7 1s.c. However, as much as we would like to have it, there is no single program, small enough to present here, for tying together the concepts and APIs presented starting with Chapter 8, "Filesystems and Directory Walks," page 227.

# 16.1 Project Description

In day-to-day use, the one program that does use just about everything in the book is the shell. And indeed, there are Unix programming books that write a small but working shell to illustrate the principles involved.

Real shells are large and messy creatures. They must deal with many portability issues, such as we've outlined throughout the book, and above and beyond that, they often have to work around bugs in different versions of Unix. Furthermore, to be useful, shells do many things that don't involve the system call API, such as maintaining shell variables, a history of saved commands, and so on. Providing a complete tour of a full-featured shell such as Bash, ksh93, or zsh would take a separate volume.

Instead, we suggest the following list of steps for writing your own shell, either as a (large) exercise to cement your understanding or perhaps as a cooperative project if you're in school.

+   1.  Design your command "language" so that it will be easy to interpret with simple code. While compiler and interpreter technology is valuable when writing a production shell, it's likely to be overkill for you at this stage. Consider the following points:

+   * Are you going to use i18n facilities?
+   * What commands must be built in to the shell?
+   * To be useful, your shell will need a command search path mechanism, analogous to $PATH of the regular shell. How will you set it?
+   * What I/O redirections do you wish to support? Files only? Pipes too? Do you wish to be able to redirect more than file descriptors 0, 1, and 2?
+   * Decide how quoting will work: single and double quotes? Or only one kind? How do you quote a quote? How does quoting interact with I/O redirections?