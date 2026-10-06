# 3 Less Typing

Since the beginning of time, Man has had an uneasy relationship with his keyboard. Sure, keyboards make it possible to express our precise wishes to the computer, but in our fat-fingered excitement to get stuff done, we often suffer from typos and digital fatigue.

In this adventure, we will travel down the carpal tunnel to the land of less typing. covered some of this in TLCL, but here we will look a little deeper.

# Aliases and Shell Functions

The first thing we can do to reduce the number of characters we type is to make full use of aliases and shell functions. Aliases were created for this very purpose and they are often a very effective solution. Shell functions perform in many ways like aliases but allow a full range of script-like capabilities such as programmatic logic, and option argument processing.

Most Linux distributions provide some set of alias definitions and it's easy to add more. To see the aliases we already have, we enter the alias command without arguments:

```
me@linuxbox: ~ alias
alias egrep='grep --color=auto'
alias fgrep='grep --color=auto'
alias glrep='grep --color=auto'
alias ls='ls --color=auto'
```

On this example, we see alias is used to activate color output for commonly used commands. It is also common to create aliases for various forms of the ls command:

```
alias ll='ls -l'
alias la='ls -A'
alias l='ls -CF'
alias l.*='ls -d .'
alias imme='ls -l | less'
```

Aliases are good for lots of things, for example, here one's useful for Debian-style systems:

```
alias update=sudo apt-get update && sudo apt-get upgrade
```

Aliases are easy to create. It's usually just a matter of appending them to our .bashrc before creating a new alias, it's a good idea to first test the proposed name of the alias with the type command to check if the name is already being used by another program or alias.

While being easy, aliases are somewhat limited. In particular, aliases can't handle complex logic or accept positional parameters. For that we need to use shell functions.