You tell pdksh to execute a Linux command whenever it encounters the alias. For example, if you have a file in your directory that holds a list of things that you must do each day, and you typically edit the file every morning to update it, you could find yourself entering the following command on a regular basis:

```
vi things-to-do-today.txt
```

Because you are entering this command quite often, you may want to create an alias for it to save yourself some typing. So instead of typing this command every time you want to edit the file, you can create an alias called ttd that causes the longer command to be executed.

To set up an alias such as this, use the pdksh alias command. To create the ttd alias, enter the following command at the pdksh command prompt:

```
alias ttd='vi things-to-do-today.txt'
```

From the time that you enter the alias command until the time you exit from pdksh, the ttd command causes the longer command to be executed. If you decide after you enter an alias that you no longer want that alias, you can use the pdksh unalias command to delete the alias:

```
unalias ttd
```

After you use the unalias command to remove an alias, the alias no longer exists and trying to execute it causes pdksh to display Command not found.

The following are some aliases that you may want to define:

```
alias ll='ls -l'
alias log='logout'
alias ls='ls -F'
```

If you are a DOS user and you prefer to use DOS file commands, you may also want to define the following aliases:

```
alias dir='ls'
alias copy='cp'
alias rename='mv'
alias md='mkdir'
alias rd='rmdir'
```