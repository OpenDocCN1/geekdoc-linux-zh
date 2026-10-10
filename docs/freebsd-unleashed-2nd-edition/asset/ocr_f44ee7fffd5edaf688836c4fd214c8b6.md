Also, unlike with a hard link, if you delete the original file that a soft link points to, the file’s data blocks are removed and the link becomes an orphan that no longer works. However, if you delete the link with rm, the original file remains untouched.

> **TIP**
> If are trying to access a file and you keep getting No such file or directory errors, and yet when you do an ls, the file is clearly there, you are probably trying to use a soft link that has become an orphan, meaning that its target (or parent) no longer exists. Use the -l option to ls and see whether the file is a soft link. If it is, check to see whether the file it points to actually exists. Note that deleting or even simply moving a file can cause its soft links to become orphans.

As a general rule of thumb, use hard links if you are pointing to a file located on the same filesystem as the one you are currently on. Hard links have the advantages of providing you with information about the actual files and of not becoming orphans if the original files are deleted or moved. However, if you need to link to a directory or link to a file that is located on a different filesystem, you must use soft links.

> **NOTE**
> Hard links also have one other advantage over soft links: They don’t take up an i-node. This may not seem like a huge issue, but there’s a fixed number of i-nodes available on the hard disk. It is possible to run out of i-nodes if you have a lot of very small files on the disk, even if you have a lot of space left on the hard disk. When you run out of i-nodes, no more files can be created until you have deleted some files and thus freed up some i-nodes.

# Universal Options

Most (but not all) of the commands mentioned in this section support the options shown in Table 7.7.

**TABLE 7.7** Universal Options for Most Shell Commands
| Option | Result |
| - | - |
| -i | Runs in interactive mode, prompting you before taking action on each file if that action would cause damage to an existing file. |
| -v | Is verbose about what the command is doing. In other words, this option prints messages on the screen for each operation as the command performs it. |
| -f | Forces the action without asking, even if the file permissions prohibit the action (for example, this action could be used to delete a file without asking whether the file is set to read-only, assuming that you have write privileges in the directory where the file is located). |