There’s a great deal more depth to Vi than is presented here; the editor is quite capable, and some Linux users are very attached to it. Entire books have been written about Vi. Consult one of these, or a Vi Web page like [http://www.vim.org](http://www.vim.org), for more information.

# Saving Changes

To save changes to a file, type `:w` from command mode. This enters ex mode and runs the `w` ex-mode command, which writes the file using whatever filename you specified when you launched Vi. Related commands enable other functions:

+   * **Edit new file** The `:e` command edits a new file. For instance, `:e /etc/initab` loads `/etc/initab` for editing. Vi won’t load a new file unless the existing one has been saved since its last change or unless you follow `:e` with an exclamation mark (`!`).
+   * **Include existing file** The `:r` command includes the contents of an old file in an existing one.
+   * **Execute an external command** The ex-mode command `:!` executes the external command that you specify. For instance, typing `:!ls rns | ls` enables you to see what files are present in the current directory.
+   * **Quit** Use the `:q` command to quit from the program. As with `:e`, this command won’t work unless changes have been saved or you append an exclamation mark to the command (as in `:q!`).

You can combine ex commands such as these to perform multiple actions in sequence. For instance, typing `:wq` writes changes and then quits from Vi.

# Criteria for Completion

To complete this task, you must successfully edit a copy of your `lilo.conf` file to add a new kernel. You don’t need to test the copy of the file, but you should verify that it’s been modified as you desired. To do so, use `cat` or `less`.

# Task 1.6: Manage Accounts

As a multi-user OS, Linux requires that users have accounts. This requirement is part of Linux’s security system, so you shouldn’t try to bypass account management or give it short shrift—say, by letting many people share an account. Instead, you should learn how to create, delete, and otherwise manage Linux accounts.

![](bbox=[0.14, 0.94, 0.3, 0.99])

Most Linux distributions provide GUI tools for account management. Although these tools are perfectly capable of handling routine account maintenance tasks on small systems, they differ from one distribution to another. The text-based tools described here are much more consistent across distributions and are the tools tested on Linux certification exams.