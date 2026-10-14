# Shell Overview

This chapter introduces you to the operating system shells. After completing this chapter, you will be able to:

+   - Understand the purpose and general features of the C shell and the Bourne, Korn, and POSIX shells
+   - Change your shell
+   - Use command entry aids common to all shells
+   - Understand your shell environment as well as the role of login scripts, environment variables, and shell variables
+   - Set and clear environment and shell variables
+   - Understand how the shell finds commands on your system
+   - Write logout scripts
+   - Write and run basic shell procedures

This chapter covers features common to all operating system shells, with some descriptions of shell differences. For detailed information on specific C shell and Bourne, Korn, or POSIX shell features, see Chapter 8.

# 7.1 Purpose of Shells

The user interfaces to the operating system are called shells. The shells are programs that interpret the commands you enter, run the programs you have asked for, and send the results to your screen.

The operating system provides the following shells:

+   - The Bourne shell (system default)
+   - The C shell
+   - The Korn shell
+   - The POSIX shell

You may access any shell, depending upon the security restrictions in effect on your system as well as upon the licensing restrictions of the Korn shell. In any case, all shells perform the same basic function: they let you perform work on your system by executing commands.