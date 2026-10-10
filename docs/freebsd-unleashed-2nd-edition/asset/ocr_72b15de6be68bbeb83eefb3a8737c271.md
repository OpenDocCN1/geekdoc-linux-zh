![](bbox=[0.375, 0.09, 0.625, 0.29])

**FIGURE 7.1** Relationship between the hardware, kernel, and shell.

# Choosing a Shell for FreeBSD

A lot of different shells are available for FreeBSD, ranging from bare-bones models to some that are loaded with features. Some shells are very terse in the command syntax they accept, and insist that you type everything correctly; other shells allow you to repeat and edit previously used commands and automatically expand command lines with the Tab key. This chapter doesn't cover all shells but rather looks at some of the more popular ones. All shells listed here can be installed from the ports (in `/usr/ports/shells`) or packages, as described in Chapter 14, "Installing Additional Software."

# The Bourne Shell (sh) and POSIX

The earliest shell still in common use is the Bourne shell, commonly known as sh. The original Bourne shell was developed at Bell Labs by Steven Bourne for the AT&T UNIX operating system. FreeBSD, like many other versions of Unix, has replaced the Bourne shell with an enhanced version called the POSIX shell. POSIX supports command-line editing, command history, and aliases—all things that the original Bourne shell did not support. You learn more about command-line editing and command history later in this chapter.

# The C Shell (csh)

The C shell is the traditional BSD shell. The researchers at Berkeley saw all the limitations the original Bourne shell had, so they created their own shell for the BSD operating system. The C shell is so named because it has a syntax that looks a lot like the C programming language. The C shell has many enhancements over the Bourne shell because of its interactive use, including job control and command history. It also has a logout configuration file, which is something most Bourne shells (sh and its descendants) don't have. The C shell also supports a configuration file that gets read every time a new subshell that is not a login shell is started (the original Bourne shell does not support this).