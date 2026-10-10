The shell acts as an intermediary between you and the Linux *kernel*, the heart of the operating system. With knowledge of the shell, you can perform many tasks far more quickly than you could with graphical utilities. In addition, the shell provides the only means available for tasks that are not supported by graphical utilities. For these reasons, knowledge of the shell is essential for all Linux users.

Linux enables you to work with more than one shell. By far the most popular is the *GNU Bourne Again Shell* (bash), which is the default shell for most Linux distributions. Some users prefer the *C Shell* (csh), which uses the syntax of the C programming language. Still others prefer *tcsh*, an extended version of the C Shell. All three of these commonly used shells resemble each other so closely that many of the basic shell commands and the essentials of shell syntax work the same way in all three. This chapter covers the fundamentals of bash shell use.

TIP You can tell which shell you’re using by looking at the default prompt in a terminal window; bash uses $, while csh and tcsh use %. Alternatively, type **echo $SHELL** and press Enter; you’ll see the current shell’s name on the next line.

# AT A GLANCE

| How Do I | See This Entry | Example |
|---|---|---|
| Create simple aliases (nicknames) for com-plex commands that are tedious to type? | alias | `alias newfiles='ls -t1'` |
| Type more than one command on a single line? | The"Command Sequences and Groups" sec-tion later in this chapter | gunzip ballisticic .tar-gz; tar -xvf ballistic .tar |