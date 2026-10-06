# Chapter 14 Interactive and Nonstandard Shell Features

No matter the current directory, the *dir* alias prints *steve*. That's because we weren't
careful about quotes when we defined the *dir alias. Recalling that the shell performs parameter
substitution inside double quotes, the problem is that the shell evaluated

```
$${PWD#*/}
```

at the time the alias was defined. This means that the *dir* alias was essentially defined as if
we'd typed in the following:

```
$ alias dir="echo steve"
```

No wonder it didn't work!

The solution is use single rather than double quotes when defining the *dir* alias to defer
parameter substitution until the alias is executed:

```
$ alias dir='echo ${PWD#*/}'
$ pwd
/users/steve
$ dir
$ cd letters
$ dir
letters
$ cd /usr/spool
$ dir
spool
$
```

Define alias
Where are we?

Execute alias

Change directory
Execute alias again

One more try

If an alias ends with a space, the word the alias is also checked for alias substitution.
For example:

```
alias nohup="*/bin/nohup 
nohup 11
```

causes the shell to perform alias checking on the string 11 after replacing nohup with /bin/
nohup.

Quoting a command or prefacing it with a backslash prevents alias substitution. For example:

```
$ '11'
ksh: 11: command not found
$
```

The format

```
alias name
```

causes the value of the alias name to be listed, and the alias command without arguments
causes all aliases to be listed.