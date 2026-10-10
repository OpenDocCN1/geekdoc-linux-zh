misc appears in), he will apply find with one non-interactive action as follows:

```
$ find . -name 'mi*' -exec ls -l {} \
$ -rw-rw-r--1  pansasan  knights1  21  Jul 15 08:48  ./misc
$ -rw-rw-r--1  pansasan  knights1  27  Jul 15 14:54  ./Misc/misc
$ -rw-rw-r--1  pansasan  knights1  32  Jul 20 11:37  ./Admin/misc
$ -rw-rw-r--1  pansasan  knights1  75  Jul 20 15:03  ./Main/misc
```

Loosely speaking, the find command in Example 7.2 states, “Start in the current directory, and working downward, find all entries that begin with mi. As you find each entry, present its data on the screen in long list format.” Here is a breakdown of each element in the command:

+   . (the dot) means to start in the current directory, which in this example is /home/pansasan, and move recursively through the file structure

+   -name means that the names of the entries you want to find will follow

+   'mi*' indicates that the first character in each entry is m. The asterisk (*) indicates that subsequent characters do not matter. This part of the command is in single quotes because the asterisk is a metacharacter, and if it were not surrounded in single quotes, it would have a different effect on the command.

+   -exec means that after finding each entry, execute the following command on it in turn

+   ls -l {} requests a long listing of the entry. The {} argument means that as each entry is found, its name should be substituted here so that ls -l can be executed on it.

+   \; is called an escaped semicolon. It indicates that we have reached the end of the find and exec command sequences.

+   Enter submits the command sequence for parsing and execution

Again, because of the way we have coded the find/exec command combination, no interaction occurs between the process and the terminal. In this case, this situation is desirable because the second action (ls -l) is not really a drastic action.

In Linux and other more recent versions of UNIX, you can use ls as an option with find. Thus, you can use an abbreviated syntax to get the