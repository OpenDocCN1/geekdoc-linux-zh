**Table 8–1: C, Bourne, Korn, and POSIX Shell Features (cont.)**

| Feature | Description | C | Bourne | Korn or POSIX |
|---|---|---|---|---|
| File name completion | A feature that lets you enter a portion of a file name and the system automatically completes it or suggests a list of possible choices. | Yes | No | Yes |
| Command line editing | A feature that lets you edit a current or previously entered command line. | Yes | No | Yes |
| Array | The ability to group data and call it by a name. | Yes | No | Yes |
| Integer arithmetic | The ability to perform arithmetic functions within the shell. | Yes | No | Yes |
| Job control | Facilities for monitoring and accessing background processes. | Yes | No | Yes |

For detailed information on shell features, see the appropriate shell reference pages sh(1b), sh(1p), csh(1), or ksh(1).

# ## 8.2 C Shell Features

This section describes the following C shell features:

+   - Sample .cshrc and .login scripts
+   - Metacharacters
+   - Command history and aliases
+   - Built-in variables and commands

# ### 8.2.1 Sample .cshrc and .login Scripts

The .cshrc login script sets up your C shell environment by defining variables and operating parameters for the local shell process. The .login script defines variables and operating parameters that you want executed at the beginning of your session, and that you want to be valid for all shell processes during the current login session.

When you log in, the operating system executes the .cshrc file in your home directory first, and the .login file second. The .login script is executed only when you log in. However, the .cshrc file is executed each time you create a subshell.

In the following .cshrc script, shell variables, command aliases, and command history variables are set. Table 8–2 explains each part of the script.