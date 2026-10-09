**Variables** Within a given process, such as a login shell or subshell, you can declare, initialize, read, and change variables. Some variables, called shell variables, are local to a process. Other variables, called environment variables, are available to child processes. For more information refer to “Variables” on page 1031.

**Hash table** The first time you specify a command as a simple filename (and not a relative or absolute pathname), *bash* looks in the directories specified by the **PATH** (page 359) variable to find that file. When it finds the file, *bash* records the absolute pathname of the file in its *bash table*. When you give the command again, *bash* finds it in its hash table, saving the time needed to search through the directories in **PATH**. The shell deletes the hash table when you log out and starts a new hash table when you start a session.

When you call the **hash** builtin without any arguments, it displays the hash table. When you first log in, the hash table is empty:

```
```
$ hash
hash: hash table empty
$ who am i
sam pts/2 2013-03-09 14:24 (plum)
$ hash
hits command
1 /usr/bin/who
```
```

The **hash -t** option causes *bash* to empty the hash table, as though you had just logged in.

```
```
$ hash -r
$ hash
hash: hash table empty
```
```

Having *bash* empty its hash table is useful when you move a program to a different directory in **PATH** and *bash* cannot find the program in its new location, or when you have two programs with the same name and *bash* is calling the wrong one. Refer to the *bash info* page for more information on the **hash** builtin.

# HISTORY

The history mechanism, a feature adapted from the C Shell, maintains a list of recently issued command lines, called *events*, that provides a quick way to reexecute any events in the list. This mechanism also enables you to edit and then execute previous commands and to reuse arguments from them. You can use the history list to replicate complicated commands and arguments that you used previously and to enter a series of commands that differ from one another in minor ways. The history list also serves as a record of what you have done. It can prove helpful when you have made a mistake and are not sure what you did or when you want to keep a record of a procedure that involved a series of commands.