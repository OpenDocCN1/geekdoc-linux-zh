# Special Functions (Continued)

| TRAPZERR | Runs whenever a command returns a nonzero exit status. |
| TRAPDEBUG | Runs after every command. |
| TRAPEXIT | Runs when the shell or function it is defined in exits. |

# Builtin Commands

The Z Shell has many builtins (page 161). This section lists a few of the important ones. Refer to the zbuiltins page for a complete list.

# ### alias: Shortcut for a Command

The zsh builtin is similar to the one in bash, with some added features. A zsh alias does not accept an argument (similar to bash—unlike tsh). A zsh function—similar to bash functions (page 672)—when you need to use an argument. The syntax to establish an alias is

alias [-grm1.] [name=value]

When you are creating an alias, the -g (global) option causes the shell to expand the alias no matter where it appears on a command line. Without this option, aliases are expanded only when they appear as the command name. Aliases are saved from session to session, so users typically establish aliases in a startup file (page 737). Without any arguments alias builtin lists active aliases. When you are listing aliases, the -g option lists global aliases, -r lists regular (nonglobal) -m lists all the aliases that have names matching a pattern that follows the command line, and -L displays aliases so that they are in an appropriate format to enter into a startup file:

```
zsh % alias -m "ps"
page=less -f'
pd_=cd
page=less
pages='less -s'
```

You may need to enclose the pattern in single or double quotation marks to keep the shell from expanding before running aliases. Calling alias with an argument of an active alias displays the value of that alias:

```
zsh % alias pages
pages='less -s'
```