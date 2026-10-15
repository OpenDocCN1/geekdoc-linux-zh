
## Aliasing Commands

You can also use the name of a command as an alias. This can be helpful in cases where you should use a command only with a specific option. In the case of the rm, cp, and mv commands, the -i option should always be used to ensure an existing file is not overwritten. Instead of constantly being careful to use the -i option each time you use one of these commands, the command name can be aliased to include the option. In the next example, the rm, cp, and mv commands have been aliased to include the -i option:

```
$ alias rm='rm -i'
$ alias mv='mv -i'
$ alias cp='cp -i'
```

The alias command by itself provides a list of all aliases that have been defined, showing the commands they represent. You can remove an alias by using the unalias command. In the next example, the user lists the current aliases and then removes the lsa alias:

```
$ alias
lsa=ls -F
list=ls
rm=rm -i
$ unalias lsa
```

## Controlling Shell Operations

The BASH shell has several features that enable you to control the way different shell operations work. For example, setting the noclobber feature prevents redirection from overwriting files. You can turn these features on and off like a toggle, using the set command. The set command takes two arguments: an option specifying on or off and the name of the feature. To set a feature on, you use the -o option, and to set it off, you use the +o option. Here is the basic form:

```
$ set -o feature      turn the feature on
$ set +o feature      turn the feature off
```

Three of the most common features are ignoreeof, noclobber, and noglob. Table 9-1 lists these different features, as well as the set command. Setting ignoreeof enables a feature that prevents you from logging out of the user shell with CTRL-D. CTRL-D is not only used to log out of the user shell, but also to end user input entered directly into the standard input. CTRL-D is used often for the Mail program or for utilities such as cat. You could easily enter an extra CTRL-D in such circumstances and accidentally log yourself out. The ignoreeof feature prevents such accidental logouts. In the next example, the ignoreeof feature is turned on using the set command with the -o option. The user can now log out only by entering the logout command.

```
$ set -o ignoreeof
$ CTRL-D
Use exit to logout
$
```

## Environment Variables and Subshells: export

When you log in to your account, Linux generates your user shell. Within this shell, you can issue commands and declare variables. You can also create and execute shell scripts. When you execute a shell script, however, the system generates a subshell. You then have two shells, the one you logged into and the one generated for the script. Within the script shell, you could execute another shell script, which would have its own shell. When a script has finished execution, its shell terminates and you return to the shell from which it was executed. In this sense, you can have many shells, each nested within the other. Variables you define within a shell are local to it. If you define a variable in a shell script, then, when the script is run, the variable is defined with that script’s shell and is local to it. No other shell can reference that variable. In a sense, the variable is hidden within its shell.

You can define environment variables in all types of shells including the BASH shell, the Z shell, and the TCSH shell. The strategy used to implement environment variables in the BASH shell, however, is different from that of the TCSH shell. In the BASH shell, environment variables are exported. That is to say, a copy of an environment variable is made in each subshell. For example, if the EDITOR variable is exported, a copy is automatically defined in each subshell for you. In the TCSH shell, on the other hand, an environment variable is defined only once and can be directly referenced by any subshell.

In the BASH shell, an environment variable can be thought of as a regular variable with added capabilities. To make an environment variable, you apply the export command to a variable you have already defined. The export command instructs the system to define a copy of that variable for each new shell generated. Each new shell will have its own copy of the environment variable. This process is called exporting variables. Thinking of exported environment variables as global variables is a mistake. A new shell can never reference a variable outside of itself. Instead, a copy of the variable with its value is generated for the new shell.

> NOTE You can think of exported variables as exporting their values to a shell, not to themselves. For those familiar with programming structures, exported variables can be thought of as a form of "call by value."

## Configuring Your Shell with Shell System Variables

When you log in to your account, the system generates a shell for you. This shell is referred to as either your login shell or your user shell. When you execute scripts, you are generating subshells of your user shell. You can define variables within your user shell, and you can also define environment variables that can be referenced by any subshells you generate. Linux sets up system shell variables you can use to configure your user shell. Many of these system shell variables are defined by the system when you log in, but you define others yourself. See Table 9-1 for a list of the commonly used ones.
