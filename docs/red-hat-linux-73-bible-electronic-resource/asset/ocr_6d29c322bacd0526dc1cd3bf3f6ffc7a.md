# # Understanding the Red Hat Linux Shell

Before icons and windows took over computer screens, you typed commands to run most computers. On UNIX systems, from which Red Hat Linux was derived, the program used to interpret and manage commands was referred to as the shell.

The shell provides a way to run programs, work with the file system, compile computer code, and manage the computer. Although the shell is less intuitive than common GUIs, most Linux experts consider the shell to be much more powerful than GUIs. Because shells have been around for so long, many advanced features have been built into them. Many old-school Linux administrators and programmers primarily use a GUI in their work as a means of opening lots of shells.

The Red Hat Linux shell illustrated in this chapter is called the *bash* shell, which stands for Bourne Again Shell. The name is derived from the fact that *bash* is compatible with the first UNIX shell: the Bourne shell (represented by the *sh* command). Other popular shells include the C Shell (*csh*), which is popular among BSD UNIX users, and the Korn Shell (*ksh*), which is popular among UNIX System V users. Linux also has a *tcsh* shell (a C shell look-alike) and an *ash* shell (another Bourne shell look-alike).

Although most Red Hat Linux users have a preference for one shell or another, when you know how to use one shell, you can quickly learn any of the others by occasionally referring to the shell's man page (for example, type *man bash*). In Red Hat Linux, the *bash* shell is roughly compatible with the *sh* shell.

> **CAUTION:** When you run the *sh* shell in Linux, a link to the *bash* shell is actually invoked, instead of the *sh* shell. To have *bash* behave like an *sh* shell when the *sh* shell is run, *bash* uses the `/etc/profile` and `~/.profile` files to configure the shell. Likewise, when *csh* is run, the *tcsh* shell is invoked instead.

# # Using the Shell in Red Hat Linux

When you type a command in a shell, you can also include other characters that change or add to how the command works. In addition to the command itself, these are some of the other items that you can type on a shell command line:

+   - **Options** — Most commands have one or more options you can add to change their behavior. Options typically consist of a single letter, preceded by a dash. You can also often combine several options after a single dash. For example, the command *ls -1a* lists the contents of the current directory. The *-1* asks for a detailed (long) list of information, and the *-a* asks that files beginning with a dot (.) also be listed. When a single option consists of a word or abbreviation, it is usually preceded by a double dash (--). For example, to use the help option on many commands, you would enter --*help* on the command line.