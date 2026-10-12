example, if you do a lot of work with files in the `/work/time/files/info/memos` directory, you could set the following variable:

```
```bash
M=/work/time/files/info/memos ; export M
```
```

You could make that your current directory by typing `cd $M`. You could run a program from that directory called hotdog by typing `$M/hotdog`. You could edit a file from there called bun by typing `vi $M/bun`.

# Adding aliases

Setting aliases can save you even more typing than setting environment variables. With aliases, you can have a string of characters execute an entire command line. You can add and list aliases with the `alias` command. Here are some examples:

```
```bash
alias p='pwd ; ls -CF'
alias rm='rm -i'
```
```

In the first example, the letter `p` is assigned to run the command `pwd`, and then to run `ls -CF` to print the current working directory and list its contents in column form. The second runs the `rm` command with the `-i` option each time you simply type `rm`. (This is an alias that is often set automatically for the root user, so that instead of just removing files, you are prompted for each individual file removal. This prevents you from removing all the files in a directory by mistakenly typing something such as `rm *`.)

While you are in the shell, you can check which aliases are set by typing the `alias` command. If you want to remove an alias, you can type `unalias`. (Remember that if the `alias` is set in a configuration file, it will be set again when you open another shell.)

# Working with the Red Hat Linux File System

The Red Hat Linux file system is the structure in which all the information on your computer is stored. Files are organized within a hierarchy of directories. Each directory can contain files, as well as other directories.

If you were to map out the files and directories in Red Hat Linux, it would look like an upside-down tree. At the top is the root directory, which is represented by a single slash ( `/` ). Below that is a set of common directories in the Linux system, such as `/bin`, `/dev`, `/home`, `/lib`, and `/tmp`, to name a few. Each of those directories, as well as directories added to the root, can contain subdirectories.

Figure 3-2 illustrates how the Linux file system is organized as a hierarchy. To illustrate how directories are connected, Figure 3-2 shows a `/home` directory that contains subdirectories for three users: `chris`, `mary`, and `tom`. Within the `chris` directory are three subdirectories: `briefs`, `memos`, and `personal`. To refer to a file called `inventory` in the `chris/memos` directory, you could type the full path of `/home/chris/memos/inventory`. If your current directory were `/home/chris/memos`, you could refer to the file as simply `inventory`.