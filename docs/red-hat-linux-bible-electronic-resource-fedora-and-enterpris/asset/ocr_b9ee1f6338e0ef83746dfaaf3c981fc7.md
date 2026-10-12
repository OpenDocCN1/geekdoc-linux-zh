each individual file removal. This prevents you from removing all the files in a directory by mistakenly typing something such as `rm *.`)

While you are in the shell, you can check which aliases are set by typing the alias command. If you want to remove an alias, you can type `unalias`. (Remember that if the alias is set in a configuration file, it will be set again when you open another shell.)

# # Working with the Red Hat Linux File System

The Red Hat Linux file system is the structure in which all the information on your computer is stored. Files are organized within a hierarchy of directories. Each directory can contain files, as well as other directories.

If you were to map out the files and directories in Red Hat Linux, it would look like an upside-down tree. At the top is the root directory, which is represented by a single slash (`/`). Below that is a set of common directories in the Linux system, such as `/bin`, `/dev`, `/home`, `/lib`, and `/tmp`, to name a few. Each of those directories, as well as directories added to the root, can contain subdirectories.

Figure 4-1 illustrates how the Linux file system is organized as a hierarchy. To illustrate how directories are connected, Figure 4-1 shows a `/home` directory that contains subdirectories for three users: `chris`, `mary`, and `tom`. Within the `chris` directory are subdirectories: `briefs`, `memos`, and `personal`. To refer to a file called `inventory` in the `chris/memos` directory, you could type the full path of `/home/chris/memos/inventory`. If your current directory were `/home/chris/memos`, you could refer to the file as simply `inventory`.

![](bbox=[0.13, 0.54, 0.7, 0.8])

**Figure 4-1:** The Red Hat Linux file system is organized as a hierarchy of directories.

Some of the Red Hat Linux directories that may interest you include the following:

+      - `/bin` — Contains common Linux user commands, such as `ls`, `sort`, `date`, and `chmod`.