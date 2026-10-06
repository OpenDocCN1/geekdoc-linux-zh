# 34 Part I ♦ Linux First Steps

Many features of the original csh, such as command-line editing and its history mechanism, are included in tcsh as well as in other shells. While you can run both csh and tcsh on most Linux systems, both commands point to the same executable file. In other words, starting csh actually runs the tcsh shell in compatibility mode.

# Using ash

The ash is a lightweight version of the Berkeley UNIX shell. It doesn't include many of the sh shell's basic features, and is missing such features as command-histories. Kenneth Almquist created the ash.

The ash is a good shell for embedded systems that have fewer resources available. The ash shell is about one-sixth the size of bash (around 100k versus 680k for bash). Because of cheaper memory prices these days, many embedded and small Linux systems have enough space to include the full bash shell.

# Using ksh

The ksh was created by David Korn at AT&T Bell Labs and is the predecessor of the sh shell. It became the default and most commonly used shell with UNIX V systems. The open source version of ksh was originally available in many rpm-based systems (such as Fedora and Red Hat Enterprise Linux) as part of the pdksh package. Now, however, David Korn has released the original ksh shell as open source, so you can look for it as part of a ksh software package in most Linux systems.

# Using zsh

The zsh shell is another clone of the sh shell. It is POSIX-compliant (as is bash), but includes some different features, such as spell checking and a different approach to command editing. The first Mac OS X systems use zsh as the default shell, although now bash is used by default.

# Exploring the Shell

Once you have access to a shell in Linux, you can begin by typing simple commands. The "Using the Shell in Linux" section later in this chapter provides more details about options, arguments, and environment variables. For the time being, the following sections will help you poke around the shell bit.