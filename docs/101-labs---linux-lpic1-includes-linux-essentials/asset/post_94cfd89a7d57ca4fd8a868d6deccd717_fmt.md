
## LAB 8: Using the Command Line to Get Help

**Lab Objective:**

Learn how to read various manuals from the command line.

**Lab Purpose:**

In a world of `Google`, `Stack Overflow`, and `Wikipedia`, sometimes we forget that Linux comes with its own library of documentation!

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough

**Task 1:**

In Linux, there are three fairly reliable ways to obtain information on a given tool. Not every tool has all three options available. The `date` command does, so we will use it as an example.

Open the Terminal application, then enter: `date --help`

This is the quick, concise way of finding information about a given command. Most commands support either the `-help` or `-h` flags. Sometimes, though, you will run into a command that doesn’t, or you just need more information than the quick help offers...

**Task 2:**

Enter: `man date`

`man` is short for `manual`, and is the most common way to provide documentation. Unlike quick help flags, it also is not limited to commands—you can use `man` pages to get information about `system` and `library` calls, special files, file formats, and even `man` itself (try entering `man man`).

**Task 3:**

Enter: `info date`

When even `man` isn't enough, sometimes you may need to rely on `info`. `info` is not the most convenient tool for casual browsing, but it provides the most details on any given aspect of a Linux system.

**Notes:**

Using unknown flags, like `--help` and `-h`, could potentially be risky, especially when a command is run as `root`. Do you understand why?

## LAB 9: Using Directories and Listing Files: Files

**Lab Objective:**

Learn how to create, delete, and list files.

**Lab Purpose:**

In this lab, you will learn how to create, delete, and list files using the `Bash` shell.

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough

**Task 1:**

Open the Terminal application, then enter: `touch foo`

You have now created a file, whose (empty) contents you can print with `cat foo`

You can list more details about the new file with `ls -lh foo`

**Task 2:**

Now create another empty file: `touch .bar`

You can use the `ls` command by itself to list all files in the current `directory` (which right now should be your `home directory`). But what happens when you do this now? Where is `.bar`?

`.bar` is a `hidden file`! Use `ls -a` and it will show up.

**Task 3:**

Now let’s clean up. Enter `rm foo .bar` to remove both files you created.

**Notes:**

When you typed `ls -a`, you probably noticed some other strange dotted entries, like `.` and `..`—these are not files, but directories, and will be covered in the next lab.

## LAB 10: Using Directories and Listing Files: Directories

**Lab Objective:**

Learn how to create, delete, enumerate, and navigate directories.

**Lab Purpose:**

In this lab, you will learn how to create, delete, enumerate, and navigate amongst directories using the `Bash` shell.

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough

**Task 1:**

Open the Terminal application, then enter: `mkdir -p foo/bar`

You have now created not one, but two directories, one inside the other. Now run the following:

```bash
cd foo
ls
```

Just like with files, you can also create hidden directories:

```bash
mkdir .baz
ls
ls -alh
```

Your `current directory` (which you changed with `cd`) is `foo`, which you can confirm with `pwd`.

**Task 2:**

`ls -alh` lists `bar` and `.baz`, as expected, but it also lists `.` and `..`—these represent the listed and parent directories, respectively. In other words, `.` is `foo`, and `..` is your home directory, also known as `~`

Now run:

```bash
cd .
pwd
pushd ..
pwd
popd
pwd
cd ~
pwd
```

How do those commands affect your navigation through the directory structure?

**Task 3:**

Now run:

```bash
cd ./foo
touch ~/foo/.baz/quux
ls -aR ~/foo
```

The `~` expands to `/home/user` (where “user” is whatever your username is). Thus, while the first command above uses a relative pathname, where the result depends on the current directory, the latter two commands use an absolute pathname. The results of those commands will be the same regardless of your directory location (unless, of course, you switch users).

**Task 4:**

Finally, let’s clean up:

```bash
cd ~
rm -r foo
```

**Notes:**

A “trick” you may run into is a file that begins with `-`, tricking `Bash` into thinking you are providing a flag to `rm` rather than the file to be removed. Can you figure out how to remove such a file?

## LAB 11: Creating, Moving, and Deleting Files

**Lab Objective:**

Learn how to copy, move, and manage larger numbers of files.

**Lab Purpose:**

In this lab, you will learn the difference between copying and moving a file, and how simple shell globbing works.

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough

**Task 1:**

Open the Terminal application, then enter:

```bash
mkdir lab11
cd lab11
touch f1 f2 f3
```

You now have a single directory containing three empty files.

**Task 2:**

```bash
cp f1 f4
ls
```

As expected, the `cp` command has created a fourth empty file. However, what happens when you do the following?

```bash
cp f1 f3
```

The `f3` file gets overwritten—hope you didn't have any important data in there!

To prevent this, use either the `-i` or `-n` flag. `-i` stands for `interactive`, which means you will be prompted before overwriting. `-n` stands for `no-clobber`, which means the target file will never be overwriten. However, `cp` won't warn you about this, so `-i` is recommended for general shell usage.

**Task 3:**

Now run:

```bash
mv f1 f5
```

`mv` is the move command, so this does what you might expect, effectively renaming `f1` to `f5`. Like `cp`, `mv` also has `-i` and `-n` flags, which have the same effects.

**Task 4:**

Now run:

```bash
mkdir foo bar
mv f2 foo
mv f3 foo
mv f* bar
```

What do you predict the final directory structure will look like? Now check it with `ls -aR bar`—did it match your prediction? (See **Answer 1** below.)

What you did with `f*` is called `globbing`. That command matched every file `and` directory starting with `f` (but not `F`—like everything else in Linux, globbing is case-sensitive), so `f4`, `f5`, and `foo` were all moved into `bar`.

**Task 5:**

Copy `foo` back to the current directory, with `cp bar/foo ./`

... Whoops! What happened? In order to copy a directory with its contents, you must use the `-r` flag (for `recursive`): `cp -r bar/foo ./`

**Task 6:**

Finally, let's clean up:

```bash
cd ~
rm -r lab11
```

### Answer 1:

```text
bar:
. .. f4 f5 foo
bar/foo:
. .. f2 f3
```

**Notes:**

Be careful with `rm -r`—that command removes an entire directory without prompting you. Many horror stories can be found on the internet of people inadvertently deleting important files when they weren’t paying attention!

## LAB 12: Archiving Files on the Command Line

**Lab Objective:**

Learn how to create, extract, and examine various types of archive files.

**Lab Purpose:**

In this lab, you will learn about `zip`, `gzip`, `bzip2`, and `xz` compressed archives—as well as a tool, called `tar`, to manage most Linux archive types.

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough

**Task 1:**

Open the Terminal application and run the following:

```bash
mkdir lab12
cd lab12
touch f1 f2 f3 f4 f5 f6 f7 f8 f9
```

**Task 2:**

If you've worked with `Windows`, you may be familiar with `ZIP` files. `ZIP` is a common type of archive which both compresses and stores files.

Run:

```bash
zip files.zip f*
unzip -l files.zip
```



You can see that all nine files are included in `files.zip`, although since they were empty there was nothing to compress. You can unzip this archive with `unzip files.zip`, but you will be prompted to overwrite the existing files.
