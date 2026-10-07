# CHAPTER 2

# COMMAND SYNTAX

You may already be familiar with many of the elements of UNIX command lines. This chapter makes sure you understand how the KornShell recognizes the significant parts of individual commands.

# CHAPTER OBJECTIVES

+   In this chapter, you will learn about:
- Command Parts Page 48
- Command Types Page 61
- Redirecting Standard Input and Output Page 84

In essence, the shell spends its life repeatedly doing just two things:

+   1. Obtaining a string of text, called a command line.
2. Executing the command line.

The shell can read command lines interactively from a user's keyboard, it can read them from a file (called a shell script or shell program), or it can receive one command line as a parameter when it starts executing. When the shell is in an interactive mode, Step 1 includes writing some text, called a prompt string, on the user's screen before reading a command line. However, Step 2 is the same, regardless of how the command line was obtained.

Before executing anything, the shell breaks a command line into individual commands, then it executes those commands. Often, there is just one command in a command line, but there are also several useful ways to put than one command in a command line. This chapter starts with individual commands, and the next chapter goes on command lines with multiple commands in them.