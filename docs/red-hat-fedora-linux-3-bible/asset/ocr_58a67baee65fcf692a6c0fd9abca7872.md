# ## Understanding the Linux Shell

Before icons and windows took over computer screens, you typed commands to run most computers. On UNIX systems, from which Linux was derived, the program used to interpret and manage commands was referred to as the *shell*.

The shell provides a way to run programs, work with the file system, compile computer code, and manage the computer. Although the shell is less intuitive than common GUIs, most Linux experts consider the shell to be much more powerful than GUIs. Because shells have been around for so long, many advanced features have been built into them. Many old-school Linux administrators and programmers primarily use a GUI as a way to open lots of shells.

The Linux shell illustrated in this chapter is called the *bash* shell, which stands for Bourne Again Shell. The name is derived from the fact that bash is compatible with the first UNIX shell: the Bourne shell (represented by the *sh* command). Other popular shells include the C Shell (*csh*), which is popular among BSD UNIX users, and the Korn Shell (*ksh*), which is popular among UNIX System V users. Linux also has a *tcsh* shell (a C shell look-alike) and an *ash* shell (another Bourne shell look-alike).

> NOTE While you can invoke the Bourne shell with `/bin/sh`, the command actually runs the bash shell in sh compatibility mode. Running `/bin/sh` produces a shell that behaves more like sh than bash, but you will probably be able to use bash scripting concepts that the real Bourne shell wouldn't recognize.

Although most Linux users have a preference for one shell or another, when you know how to use one shell, you can quickly learn any of the others by occasionally referring to the shell’s man page (for example, type *man bash*). In Linux, the bash shell is roughly compatible with the *sh* shell.

# ## Using the Shell in Linux

When you type a command in a shell, you can also include other characters that change or add to how the command works. In addition to the command itself, these are some of the other items that you can type on a shell command line:

+   * **Options** — Most commands can one or more options you can add to change their behavior. Options typically consist of a single letter, preceded by a dash. You can also often combine several options after a single dash. For example, the command `ls -la` lists the contents of the current directory. The `-l` asks for a detailed (long) list of information, and the `-a` asks that files beginning with a dot ( . ) also be listed. When a single option consists of a word, it usually preceded by a double dash ( -- ). For example, to use the help option on many commands, you would enter --help on the command line. Here’s an example of help information for the `ls` command (Output is piped to the `less` command to page through it; type `q` to quit):

```
```
$ ls --help | less

Usage: ls [OPTION]... [FILE]...  
List information about the FILEs (the current directory by default).

-1          display the file contents  
-a, --all   do not ignore entries starting with .  

... more options 
```

```