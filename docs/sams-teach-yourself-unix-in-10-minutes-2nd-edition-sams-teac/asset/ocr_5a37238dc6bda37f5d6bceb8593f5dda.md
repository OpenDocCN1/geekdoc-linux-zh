that shells provide to the user the capability to create command aliases.
As you can see, the commands can get completely out of hand as you use REs and options to build it and make it more effective.

Aliases are quite simple, aliases. If, for example, you're a longtime DOS user, you might find yourself typing del instead of rm to delete files. Want to change this? set an alias with the alias command. The syntax is as follows: alias <newname> <command to run>. If you actually want to make aliases for del, type the following: alias rm. After setting this alias, any time you type del, it executes the command rm. This is actually something commonly done on many different systems.

More useful than renaming commands, you can use the alias command to create meta commands that enforce certain options. For example, it's always a good idea to fix rm to be in interactive mode (rm -i). To do this with an alias, you can type the following: alias rm 'rm -i'. (Note the direction of single quotes.) Now when you type rm actually executes rm -i instead.

Remember, aliasing is done to help you shorten your typing workload. If you find yourself in situations where you are typing out long strings often and all start to look identical, then it would make sense to create aliases to save you some time.

# Environment Variables

Earlier in this book, we touched on the concept of environmental variables in Unix. In Lesson 14, "Shell Scripting Fundamentals," variables used in the shell were discussed. To explain how environmental variables are used, consider how your Unix system runs. Most of the programs are run based on text files that help build the command into the environment for use. If you don't have a file, then most likely you will be setting a program up with an environmental variable. The environmental variable will essentially be where the program draws its configuration information from.

Environment variables are used by programs to pick up specific pieces of information that are needed when the program is run. For example, you