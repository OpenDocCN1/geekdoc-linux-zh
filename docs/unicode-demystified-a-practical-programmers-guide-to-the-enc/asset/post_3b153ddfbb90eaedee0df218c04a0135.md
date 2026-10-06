
Advanced Exercises 733

- 11. Modify the foreach_1 program (page 721) so that it takes the command to
exec as an argument.
- 12. Rewrite the program while_1 (page 722) so that it runs faster. Use the time
builtin to verify the improvement in execution time.
- 13. Write your own version of find named myfind that writes output to the file findout without the clutter of error messages, such as when you do not
have permission to search a directory. The myfind command should accept
the same options and arguments as find. Can you think of a situation in
which myfind does not work as desired?
- 14. When the foreach_1 script (page 721) is supplied with 20 or fewer
arguments, why are the commands following tomany: not executed?
(Why is there no exit command?)

# IN THIS CHAPTER

- Z Shell Basics 736
- Variables 741
- Builtins 767
- Command Line Editing 791
- Shell Programs 808
- Z Shell Options 824

## The Z Shell and Advanced Shell Programming

The Z Shell (zsh) combines many features of the Bourne Again, TC, and C Shells. In addition, zsh incorporates a number of new features. Because of the large number of features and configuration options available in zsh, this chapter concentrates on the most common and skips some of the more obscure ones. This chapter also explains how to customize zsh to meet your needs. If you have used csh or tsh before, you can configure zsh to behave the same way as csh and tsh. If you have used the Korn Shell, setting up zsh to work like ksh may be useful to you.

This chapter builds on the material presented in the earlier chapters on shells and shell programming. If you read Chapters 12 through 14.

After an introduction, this chapter starts with a discussion of variables and shell builtins. Next is a discussion of command line editing, followed by a section on command processing that describes the various steps the shell takes when processing a command line. Then an extensive section on shell programming discusses recursion and guides you through the construction of two longer shell programs. This chapter ends with a list of Z Shell options.

## The Z Shell Is Not Automatically Installed with Red Hat

The complete set of Red Hat disks includes the zsh rpm file (page 928). You can also download it from Red Hat's Web site or www.rpmfind.net.

## The Z Shell, Korn Shell, and Pd-ksh

A complete version of the Korn Shell is now available as a commercial product for use with GNU/Linux, most users of the Korn Shell have relied on their domain implementation Pd-ksh (for Public Domain ksh; the name of the program is pdksh). Although pdksh (ww.cs.mun.ca/~michael/pdksh) provides most of the basic features of the Korn Shell, it is missing some of the more advanced-features that make the Korn Shell a powerful language for writing shell scripts. Most of these features (and some) are present in zsh. In fact, if the Z Shell is linked to the filename /bin/ksh, running /bin/ksh results in the Z Shell starting with a default configuration that closely resembles the Korn Shell.

## Z Shell Basics

If you want to use the Z Shell as your login shell, run csh and specify the path /bin/zsh as described in “Entering and Leaving the TC Shell” (page 683). Alternatively, Superuser can set up the /etc/passwd file toward the same end.

The basic behavior of the Z Shell mimics that of the other shells: You type a command that names an executable program or script, optionally followed by arguments that are interpreted by the command. You can correct mistakes by pressing the RETURN key. On page 37 you can also use the Z Shell's powerful command line editing (page 791) and history editing (page 795) to create and modify command lines.

Like bash and tsh, zsh evaluates variables, searches for aliases and functions, expands ambiguous file references, and handles redirection before executing a command. It is important to understand the precise sequence in which these steps are carried out because it affects the meaning of a command line. Before describing the steps in command line processing in detail, this chapter describes other aspects of the shell. Refer to “Processing a Command” on page 797.

## Running Scripts

To execute a Z Shell script, use the script name as an argument to zsh:

```
zsh % zsh script_name
```

The preceding command calls zsh regardless of which shell you are working with. If you have executed permission for the file that contains the script, you can use the filename as a command:

```
zsh % script_name
```

When you start the first line of the script with #!/bin/zsh, the Z Shell runs the script, regardless of what shell you call the script from (page 564):

## Startup Files

The Z Shell uses many of the same environment variables as bash and adds a few others. You can set these variables, along with commands that establish other characteristics of the Z Shell environment, in one of the Z Shell startup files (Table 15-1). All startup files with names that begin with a period reside in your home directory.

| Startup Files | table 15-1 |
| :--- | :--- |
| /etc/zenv | This file is created by Superuser systemwide default characteristics for zsh. It is the first and only file that zsh always reads when it starts. |
| ~/zenv | You create this file in your home directory. The preferred location to set variables that override those set in /etc/zenv, is the second file to be read. |
| /etc/zprofile | This file is created by Superuser to establish systemwide default characteristics for zsh login shells. It is read when a login shell starts up (or when zsh is called with the -l option) but not when you use the -f option. It is the preferred file for setting systemwide characteristics for users desiring a bash- or ksh-like shell. |
| ~/zprofile | You create this file in your home directory. This file is the preferred location to set variables that override those set in /etc/zprofile and read when a login shell starts up (or when zsh is called with the -l option) but not when the -f option is used. This file is preferred for setting personal characteristics for a bash- or ksh-like shell. |

## Startup Files (Continued)

| Startup Files | |
| :--- | :--- |
| /etc/zshrc | This file is created by Superuser to establish systemwide default characteristics for zsh interactive shells (where standard input and standard output are both connected to terminal). This file is not read when zsh is called with the -f option |
| ~/.zshrc | You create this file in your home directory. This file is read only by interactive shells (where standard input and standard output are both connected to a terminal) and is not read when zsh is called with the -f option |
| /etc/zlogin | This file is created by Superuser to establish systemwide default characteristics for zsh login shells. It is read when a login shell starts up (or when zsh is called with the -l option) but not when the -f option is used. It is the preferred file for systemwide characteristics for users desiring a C- or TC-like shell |
| ~/.zlogin | You create this file in your home directory. This file is the preferred location to set variables that override those set in /etc/zlogin and when a login shell starts up (or when zsh is called with the -l option) but not when the -f option is used. It is the preferred file for setting characteristics for users desiring a C- or TC-like shell |

Because .zenv is the only file used for zsh initialization except when you use -f), you can place all your variable initializations and option setups in this file. How you use the other startup files depends on how you use zsh: Is the invocation of zsh login shell and/or an interactive shell? Sample .zenv, .profile, and .zrc files follow. Some of the commands used in these files are not covered later in this chapter. In any of the startup files, functions that you want to be able to process:

```
% cat .zenv
MAIL=/usr/spool/mail/${LOGIN}?
MANPATH=/usr/man:/usr/X11R6:/usr/local/man
PATH=$HOME/bin:/usr/local/bin:/usr/bin/X11:/usr/bin:/bin:
export MAIL MANPATH PATH
umask 002
% cat .profile
FCEDIT=/usr/bin/vim
PS1='$ '
PS2='>
HISTSIZE=256
stty kill '^u' erase '^h' intr '^Ac' quit '^\'
export FCEDIT PS1 PS2 HISTSIZE
```
