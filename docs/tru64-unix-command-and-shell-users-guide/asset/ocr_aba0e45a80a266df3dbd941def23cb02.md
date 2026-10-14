# ### 4.1 Creating a Directory (mkdir)

Directories let you organize individual files into useful groups. For example, you could put all the sections of a report in a directory named `reports`, or the data and programs you use in cost estimating in a directory named `estimate`. A directory can contain files, other directories, or both.

Your login directory was created for you when your computer account was established. However, you probably will need additional directories to organize the files you create while working with the operating system. You create new directories with the `mkdir` (make directory) command.

The format of the mkdir command is:

```
mkdir  _dirname_
```

The _dirname_ entry is the name you want to assign to the new directory.

The system creates _dirname_ as a subdirectory of your working directory. This means that the new directory is located at the next level below your current directory.

In the following example, return to your login directory by entering the `cd` command, and create a directory named `project2`:

```
```text
$ cd
$ mkdir project2
$
```
```

Now, create a subdirectory in the reports directory by entering a relative pathname:

```
```text
$ mkdir reports/status
$
```
```

Figure 4–1 shows the new file system tree structure. The `project`, `project2`, and `reports` directories are located one level below your login directory, and the `status` subdirectory is located one level below the `reports` directory.