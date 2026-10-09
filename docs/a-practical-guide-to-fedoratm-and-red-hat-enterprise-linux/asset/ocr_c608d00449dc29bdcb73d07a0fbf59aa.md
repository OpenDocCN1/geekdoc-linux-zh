+   * The TC Shell (*tosh*), an enhanced version of the C Shell that was developed as part of BSD UNIX.
+   * The Z Shell (*zsh*), which incorporates features from a number of shells, including the Korn Shell.

Because different users might prefer different shells, multiuser systems can have several different shells in use at any given time. The choice of shells demonstrates one of the advantages of the Linux operating system: the ability to provide a customized interface for each user.

Besides performing its function of interpreting commands from a keyboard and sending those commands to the operating system, the shell is a high-level programming language. Shell commands can be arranged in a file for later execution (Linux calls these files *shell scripts*; Windows calls them *batch files*). This flexibility allows users to perform complex operations with relative ease, *often by issuing short commands, or to build with surprisingly little effort elaborate programs that perform highly complex operations.*

# FILENAME GENERATION

When you type commands to be processed by the shell, you can construct patterns using characters that have special meanings to the shell. These characters are called *wildcard* characters. The patterns, called *ambiguous file references*, are a kind of shorthand: Rather than typing in complete filenames, you can type patterns; the shell expands these patterns into matching filenames. An ambiguous file reference can save you the effort of typing in a long filename or a long series of similar filenames. For example, the shell might expand the pattern `mak?*tar.gz` to `make-3.8.0.tar.gz`. Patterns can also be useful when you know only part of a filename or cannot remember the exact spelling of a filename.

# COMPLETION

In conjunction with the Readline Library, the shell performs command, filename, pathname, and variable completion: You type a prefix and press *TAB*, and the shell lists the items that begin with that prefix or completes the item if the prefix specifies a unique item.

# DEVICE-INDEPENDENT INPUT AND OUTPUT

Devices (such as a printer or a terminal) and disk files appear as files to Linux programs. When you give a command to the Linux operating system, you can instruct it to send the output to any one of several devices or files. This diversion is called *output redirection*.

In a similar manner, a program's input, which normally comes from a keyboard, can be redirected so that it comes from a disk file instead. Input and output are *device independent*; that is, they can be redirected to or from any appropriate device.

As an example, the *cat* utility normally displays the contents of a file on the screen. When you run a *cat* command, you can easily cause its output to go to a disk file instead of the screen.