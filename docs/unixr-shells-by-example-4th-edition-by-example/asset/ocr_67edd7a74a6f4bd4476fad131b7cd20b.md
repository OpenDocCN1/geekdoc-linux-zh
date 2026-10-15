# chapter

# 9

# The Interactive
# C and TC Shells

![](bbox=[0.616, 0.043, 0.765, 0.231])

# ## 9.1  Introduction

An interactive shell is one in which the standard input, output, and errors are connected to a terminal. The C shell (csh) and TC shell (tcsh) provide a number of convenient features for interactive use that are not available with the Bourne shell, including filename completion, command aliasing, history substitution, job control, and more. These shells are almost identical when used as a programming language, but the TC shell has many more interactive features than its predecessor, the C shell. This section covers the common features of the C shell and TC shell for interactive use. If you are looking for some nice shortcuts at the command line, the new TC shell enhancements are covered in the second half of this chapter, beginning with “New Features of the Interactive TC Shell” on page 460.

# ### 9.1.1  C/TC Shell Startup

Before the shell displays a prompt, it is preceded by a number of processes. (See Figure 9.1.) After the system boots, the first process to run is called init; it is assigned process identifier number (PID) 1. It gets instructions from a file called initab (System V) or spawns a getty process (BSD). These processes are responsible for opening up the terminal ports, for providing a place where input comes from (stdin), where standard output (stdout) and error (stderr) go, and for putting a login prompt on your screen. The /bin/login program is then executed. The login program prompts for a password, encrypts and verifies your password, sets up an initial working environment, and then initiates the shell, /bin/csh or /bin/tcsh for the C or TC shell, respectively.

When the shell is a login shell, this is the sequence of invocations: The C/TC shell looks in the /etc directory for system startup files, which are executed if they exist. For the C shell, for example, these files are /etc/csh.cshrc and /etc/csh.login. (See Chapter 16, “The System Administrator and the Shell,” on page 1023 for details.) Then the C/TC shell looks in the user's home directory for a file called .cshrc or .tcshrc, respectively.