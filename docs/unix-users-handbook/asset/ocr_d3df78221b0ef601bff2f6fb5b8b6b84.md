# Aliases in .cshrc

An alias is a name that you select for a frequently used command or series of commands. Many aliases are predefined for you.

You can use the .cshrc file as a place where your aliases are stored and read every time you log in. You can also define aliases at the command-line prompt, but these are cleared when you log out.

The alias command, without any arguments, lists all aliases. This list includes both preset aliases as well as those you have set. The following alias command shows all preset aliases on the system on which I am working:

```
```
sys1 7: alias
d	dirs
m	more
pd	pushd
pd2	(pushd +2)
po	popd
status	(date; bdf)
sys1 8:
```
```

You are not restricted to using only the preset aliases. To create your own alias, you first issue the alias command, the name of the alias, and then the command or commands that are executed when the alias is executed.

Let's now create a few simple aliases. The first creates an alias of "h" for the history command:

```
```
sys1 1: alias h history
sys1 2: h
	history
```
```