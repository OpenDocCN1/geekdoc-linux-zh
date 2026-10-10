monly specified options. For more comprehensive listings, check your information sources.

# ## Entering and Editing Commands at the Command Line

Before we discuss editing at the command line, it might be useful to mention Linux/UNIX shells again. Shells are, among other things, Linux/UNIX command interpreters, and we described them in more detail in Chapter 7, “Shell Basics.”

Let’s quickly summarize by stating that when a user logs in to Linux, one of the several available shells is invoked by default according to what is found in the user’s profile in the *\textit{/etc/passwd*} file. Because many principles, utilities, and commands are similar from shell to shell, we will focus here on the Bourne Again Shell, or Bash shell. (We also learned in Chapter 7 how a user can switch from one shell to another by using some simple commands, however.)

# ## Basic Command-Line Navigation and Editing

With Bash, you type commands by using letters, numbers, and some metacharacters and then execute the commands by pressing Enter. To navigate back and forth along the command line, you can use the right arrow and left arrow keys. To delete text, you can use the Delete and Backspace keys. You can use some of the other handy keys, too, such as Home and End. The Shift, Alt, Ctrl, and function keys (that is, F1, F2, and so on) are a different story, however. Using them can provide some utility (examples: Ctrl-o presents the ls command automatically; Ctrl-p presents the last command executed; the Alt key, used with characters such as 2, 4, 7, 8, 9, 0, ¬, c, e, or \vert, can create other special characters, and so on). But sometimes, using them can produce unpredictable or inconvenient results as well.

# ## The Up and Down Keys and Command History: A Review

Remember back near the end of Chapter 7 when we introduced you to the power and convenience of the up and down keys? We can use them to tap into our command history, starting with the RAM buffer where commands