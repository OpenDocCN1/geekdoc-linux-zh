Note that rmdir can only remove directories that are empty. If there are any files or subdirectories within the directory, you will get the error message directory is not empty. Later in this hour, we will look at a command that can remove directories that are not empty.

Note that the rmdir command does not ask for confirmation before it goes to work. FreeBSD assumes that you know what you are doing and by default, commands almost never ask for confirmation before they go to work—even if you have told them to do something extremely destructive. If you are not sure what you are doing, there is a command line option to use with most commands. The option is -i. The -i is short for interactive. This causes the command to ask you for confirmation before it actually does anything. This option can be very useful when you are not entirely sure that the command you are giving FreeBSD will have the intended effect. If it turns out that the command is going to do something other than what you intended, the -i option will let you know about it and give you the opportunity to bail out before it is too late.

Assuming that you are following along and you issued the preceding rmdir command, go ahead and re-create the directory using the mkdir command again because we will use it in the next section.

# Listing Directory Contents

The ls command is used to list the contents of directories. Here is some sample output from the ls command:

```
bash$ ls
Mail      projects      proposal-draft      program1
tyfsbd    mail          program1.c
bash$
```

The main problem with this listing is that it gives you virtually no information about what kinds of things actually exist in the directory other than their names. But there is no way to tell whether the entry belongs to a file, subdirectory, and so on. Because of this, the ls command provides several options that can be used to get it to display more information on each entry. For example, the -F entry causes ls to give us more information about the type of each entry in the list:

```
bash$
Mail/      projects/      proposal-draft      program1*
tyfsbd@    mail/          program.c
bash$
```

The symbols behind some of the entries in the preceding listing tell us what kind of entry it is. Here is what they mean: