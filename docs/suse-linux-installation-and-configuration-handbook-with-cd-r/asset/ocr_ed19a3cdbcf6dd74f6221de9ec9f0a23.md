continued

| Option | Meaning |
| --- | --- |
| -S | The file exists and is a socket. |
| -t | The file exists and is open on a terminal. |
| -u | The file exists and is set uid bit. |
| -w | The file exists and is writeable. |
| -x | The file exists and is executable. |
| -O | The file exists and is owned by the current user. |
| -G | The file exists and is owned by the current group. |
| -z | The file exists and is zero bytes in length. |
| -n | The file exists and is not zero bytes in length. |

This was a brief crash course in shell scripting. Shell scripts are one of the most powerful aspects of Linux. A discussion on how to fully master them is beyond the scope of this book, but is something you should definitely seek. So much can be accomplished using a shell script, you'd be amazed. A good starting place for more information is the scripts that are available in SuSE Linux. Read /etc/profile and for more scripts, check the init scripts in /sbin/init.d—these are works of art!

# TCSH Specifics

The TCSH is another shell you can use with SuSE Linux. It is similar to bash in many ways because bash has inherited a bit of TCSH. TCSH is an improvement over the older C shell and is particularly appealing to programmers because it uses syntax that is similar to the C language. You don't have to be a programmer to know how to use the shell, but if you are, you will enjoy it even more. As an interactive shell, the TCSH is almost exactly the same as bash, but when it comes to scripts, the two differ greatly.

# Initialization Files

The TCSH has three configuration files, .login, .tcshrc, and .logout. These files work the same in TCSH as they do in the bash shell.

The .login file is executed every time you run TCSH as a login shell. This file corresponds to the .profile file used by the bash shell. The .login file should contain any environment variables you want declared when you log in. The SuSE team does not supply you with a .login file because bash is the default shell for SuSE Linux. So, you don't really have to start with this file like you do with bash's .profile.

The .tcshrc file is executed every time the shell is run, regardless of whether it's a login shell or subshell. This file is the same as the .bashrc file in bash. In this file you enter all the