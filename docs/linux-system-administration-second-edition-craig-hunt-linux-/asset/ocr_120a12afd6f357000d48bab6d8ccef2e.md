The easiest way to retrieve a command from the history list is by using the arrow keys, especially if the command was recently entered. The up arrow retrieves the previous command from the history list, and the down arrow retrieves the next command. You may traverse the entire history list this way if you wish, but if HISTSIZE is large, this can become tedious.

An alternate way to fetch a command from the history list is to enter on the command line an exclamation point followed by enough letters to uniquely identify the command you wish to retrieve. The most recent iteration of the command is then retrieved and executed. Entering `!pine` at the command line would retrieve the last pine command in the `.bash_history` file, pine myfriend@hometown.com. If you knew that you had recently used the pine command to write to otherfriend, you could type `!pine o` at the prompt and the pine otherfriend@nothome.com command would be retrieved. Entering `history` at the command line will yield a list of the commands in your current `.bash_history` file.

# Basic Commands

Although there are exceptions, basic Linux commands generally take one of the following forms:

```
```
command [-option] target
command [-option] source destination
```
```

Linux command names, like filenames, are case-sensitive. Although most commands are completely lowercase, some options are uppercase. The man pages discussed above are invaluable when using unfamiliar commands. Even someone who has been administering a system for 20 years can learn something new about the functionality of the basic commands. New options are being added all the time, as are entirely new commands.

The Linux commands presented below are some of the most commonly used. These definitions are not intended to be comprehensive but to give you a general idea of their use. Although we show the general syntax of each command listed, this is not a formal command reference, defining every option of each command. For a complete reference, see the appropriate man page. Later chapters discuss many of these commands in more detail, in the context of their administrative uses.

# User Account Commands

The commands in this section allow you to work with user accounts. They include the commands to create a user, to delete a user, and to perform various other common user functions. More information on user-specific tasks is available in Chapter 5, “Creating and Maintaining User Accounts.”

+   **adduser**

There is actually no adduser command under Red Hat; to accommodate users who have used this command in other Unix varieties, it is symbolically linked to the useradd command, explained below.

+   **finger**

```
```
finger [options] [username] [@host]
```
```

The finger command is used to display information about the system’s users. Since this command can be used remotely by giving the target user’s name as `username@host`, it is usually disabled as a security measure.