# GUIDED EXERCISE

# READING INFO DOCUMENTATION

In this exercise, you will look up information stored in GNU Info documents by navigating those documents with command-line tools.

# OUTCOMES

You should be able to navigate GNU Info documentation with command-line tools.

# BEFORE YOU BEGIN

Log in to workstation as student using student as the password.

On workstation, run the lab help-info start command.

```
[student@workstation ~$ lab help-info start
```

+   1. On workstation launch info without any arguments.

```
[student@workstation ~$ infoinfo
```

+   2. Navigate to the Common options topic.
Use UpArrow or DownArrow until (coreutils) Common options is highlighted.

+   Basics
* Bash: (bash). The GNU Bourne-Again Shell.
* Common options: (coreutils)Common options.

> Figure 4.2: Bash documentation

+   3. Press Enter to view this topic.

```
File: coreutils.info, Mode: Common options, Next: Output of entries file, Prev: Introduction, Up: Top
Common options
```

Certain options are available in all of these programs. Rather than writing descriptions for each of the programs, they are described here. (In fact, every GNU program accepts (or should accept) these options).
Normally options and operands appear in any order, and programs act as all the options appear before any operands. For example, 'sort -t :' likes 'sort -r -t :', since 'i' is an option of '-t'. However, if the 'POSIX_COR' environment variable is set, options must appear before operands, unless otherwise specified for a particular command.

> Figure 4.3: Common options info topic

+   4. Browse through this Info topic. Whether long-style options can be abbreviated.