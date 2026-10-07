# CHAPTER 22

# Shell Scripting

# IN THIS CHAPTER

+   - The Shells Included with This Book

+   - The Shell Command Line

+   - The Basics of Writing, Creating, and Executing a Shell Script

+   - Creating and Executing a Simple Shell Program with bash

+   - Using Variables in Shell Scripts

+   - Positional Parameters

+   - Built-In Variables

+   - Special Characters

+   - Comparison of Expressions

+   - Iteration Statements

+   - Conditional Statements

+   - The break and exit Statements

+   - Using Functions in Shell Scripts

+   - Reference

Fans of the point-and-click computer interface might not be familiar with or comfortable using a command line. The Linux command line, known as a shell, is an integral part of the Linux operating system. In certain situations on particular hardware, the shell might be the only way to interact with a server via dialup or over a network. The shell is much more than a command with sophisticated features; it has a syntax that is a programming language. Using that syntax, you can define variables, assign various values, compare results, and so on.

This chapter is an introduction to the basics of creating shell scripts, or executable text files to conform to shell syntax. Shell scripts run like any other command under Linux and can contain complex logic or a series of Linux command-line instructions. You can also run other shell scripts from within a shell program. The features and functions for several Linux shells are discussed in this chapter after a short introduction to working from the shell command line. You learn how to write and execute a simple shell program using bash, one of the most popular Linux shells. You also get an overview of the structure of shell syntax.

# The Shells Included with this Book

The Red Hat Linux distribution installed from the CD-ROMs that accompany this book includes a rich assortment of capable, flexible, and powerful shells. Each shell is different, but has numerous built-in commands, configurable command-line prompts, and include features such as command-line history and editing. As an example, the bash is so powerful that it is possible to write a minimal web server entirely in bash's language using 114 lines of script (see the link at the end of this chapter).