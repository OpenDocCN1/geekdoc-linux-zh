# # CHAPTER 11
## Customizing the Shell

Regardless of whether you choose to operate your FreeBSD system through the X-Window GUI—particularly as an administrator—you’re going to have to deal with a shell. A shell gives you all the flexibility you need to accomplish even the most complex tasks but also dictates a user experience that’s arcane at best. In this chapter, we’ll make ourselves at home in the shell—comfortable enough to use it as a programming environment and as a user interface.

# ## What Is a Shell?

We’ve already talked about the basics of the shell and what you can do with it back in Chapter 7, “Working with the Shell.” That chapter introduced the shell as a command-line interface and discussed the various shells you can use in FreeBSD and what kinds of commands are available in the shell for controlling the system. Now, we’ll be looking at the shell itself in more detail and examining how it applies to the multitudes of users you might be supporting on your system and how to customize it to your taste.

You already know that a shell (in brief) is a command-line interface in which you can enter the typed commands that make the Unix computing experience so markedly different from a fully GUI-based one such as Windows or Mac OS. The shell is similar in function to the COMMAND.COM command interpreter in MS-DOS and its descendants in Windows, but it’s vastly more complex and useful because it plays a much more important role than in a GUI-based operating system.

But why is it called a shell? The answer has to do with the terminology used in Unix architecture to describe the various levels of system operation in terms of a multilayered ball, with the most automated functions at the core and the user-triggered functions on the outer layer. On the inside is the

# ### IN THIS CHAPTER

+   - What Is a Shell?
+   - Adding Shells to the System and Making Them Available
+   - Using Alternate Shells
+   - Shell Initialization Files
+   - Customizing Your Shell Environment
+   - Shell and Environment Variables