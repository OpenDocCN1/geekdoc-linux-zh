![](bbox=[0.15, 0.05, 0.62, 0.28])

You can then launch a text-based application, such as the pico text editor, inside an X11 terminal window like this:

```
#  ./x11  pico
```

You’ll see a window such as that shown in Figure 9.1.

Shell aliases are also useful if you want to create abbreviated commands, shortcuts, or custom versions of commands for use from the command line after you log in to Linux. Red Hat (and other Red Hat-based distributions such as Mandrake and Yellow Dog) Linux users can define these aliases in the file .bashrc in the home directory. Here are some of the most useful (and safer) aliases to define:

```
alias rm='rm -i'
alias mv='mv -i'
alias cp='cp -i'
```

These examples create much safer versions of the rm, mv, and cp commands. The -i (interactive) option forces you to type a y or n when deleting, renaming, or potentially copying over existing files. Open your .bashrc file with a favorite text editor, and then type in these aliases. Another one you might want to create is for custom directory listings with the ls command:

```
alias ll='ls -l'
```

Save the .bashrc file, and then use the bash shell’s source command to read in the new aliases, like this:

```
# source .bashrc
```

After you become familiar with other Linux commands, you’ll be able to craft your own favorite aliases!