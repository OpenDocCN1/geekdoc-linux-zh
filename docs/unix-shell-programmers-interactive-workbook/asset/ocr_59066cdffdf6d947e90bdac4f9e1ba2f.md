# 12 Lab 1.2: Setting Up Your Interactive Environment

c) Were there any files or directories named bin or fun in your home directory?

If there were no files or directories named bin or fun in your home directory, create those directories now and verify them with the following commands:

```
mkdir bin fun
ls -ld bin fun now
```

d) Are the directories in place now?

# 1.2.2 SET UP YOUR PROFILE AND ENVIRONMENT FILE

Setting things up properly to use the KornShell involves creating or modifying some files in your home directory. Before you do that, here is some background that will help you understand the rationale for what you are going to do with these files.

When you connect to your computer system, a program, usually named login, prompts you to enter your username and password, which it looks up in the system's user database (such as a file named passwd or in the Windows registry). That database also tells login the pathname of your home directory and the pathname of your shell program.

At this point, a process starts executing your shell (ksh). In general, you can use the terms process and program interchangeably, but there are real differences between the two. For example, on most systems, login and ksh are two programs (executable files) that are executed by the same process. Processes take a