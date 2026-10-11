# Chapter Ten: UNIX SHELL SCRIPTING

Time is precious. It does not make sense to waste time typing a frequently used sequence of commands at a command prompt, more especially if they are abnormally long or complex. Scripting is a way by which one can alleviate this problem by automating these command sequences in order to make life at the shell easier and more productive. Scripting is all about making the computer, the tool, do the work. By the end of this tutorial you will have a good understanding of the kind of scripting languages available for Unix and how to apply them to your problems. UNIX contains many wonderful and strange commands that can be very useful in the world of scripting, the more tools you know the better you know them, the more use you will find for them. Most of the Unix commands and many of the built-in commands have `man` pages; `man` pages contain the usage instructions pertaining to the parent tool. They are not always very clear and may require reading several times. In order to access a man page in Unix the following command sequence is applied:

```
`man command`
```

If a man page exists for the command specified the internal viewer will be invoked and you will be able to read about the various options and usage instructions.

# Shell Scripting Introduction

UNIX uses shells to accept commands given by the user; there are quite a few different shells available. The most commonly used shells are SH (Bourne SHell) CSH (C SHell) and KSH (Korn SHell), most of the other shells you encounter will be variants of these shells and will share the same syntax, KSH is based on SH as is BASH (Bourne again shell). TCSH (Extended C SHell) is based on CSH.

The various shells all have built in functions which allow for the creation of shell scripts, that is, the stringing together of shell commands and constructs to automate repetitive tasks in order to make life easier for the user.

With all these different shells available, what shell should we use? This is debatable. For the purpose of this tutorial we will be using SH because it is practically guaranteed to be available on most Unix systems and be supported by the SH based shells. Your default shell may not be SH. Fortunately we do not have to be using a specific shell in order to exploit its features because we can specify