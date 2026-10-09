
**Answer 1:**

```
bar:
. .. f4 f5 foo
bar/foo:
. .. f2 f3
```

**Notes:**

Be careful with `rm -r`—that command removes an entire directory without prompting you. Many horror stories can be found on the internet of people inadvertently deleting important files when they weren’t paying attention!

## LAB 44

### Perform Basic File Management: Find and Globbing

**Lab Objective:**
Learn how to use advanced filename expansion in Bash, as well as the *find* command to locate and act on specific files.

**Lab Purpose:**
In this lab, you will learn about shell globbing, and how to use the *find* command to locate files based on type, size, etc. and execute commands on those files.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

#### Task 1:
It is important to understand that, although shell globbing shares some commonalities with regular expressions, Bash itself does not recognize the full regex syntax. Instead, Bash simply recognizes and expands wild cards.

Open the **Terminal** and run:

- `mkdir lab44`
- `cd lab44`
- `touch a1 a2 a12 b1 b2 b12 c1 c2 c12`

#### Task 2:
To understand how advanced globbing works, run the following commands and observe the output (on the right):

- `ls a?` a1 a2
- `ls a*` a1 a12 a2
- `ls [ab]?` a1 a2 b1 b2
- `ls [ab]*` a1 a12 a2 b1 b12 b2
- `ls [^ab]*` c1 c12 c2
- `ls ?[1-2]` a1 a2 b1 b2 c1 c2
- `ls ?[1-2]*` a1 a12 a2 b1 b12 b2 c1 c12 c2

#### Task 3:
Now, apply this shell globbing to find and execute a command on a certain set of files (copy and paste won't work for the below):

```bash
find . -name "c?" -execdir ls -l {} \;
```

What this command is doing is searching in the current directory (recursively) for all files named "c?", which in this case matches c1 and c2. It then effectively executes `ls -l [file]` on each file found. The `{}` syntax references the filename, while the escaped semicolon denotes the end of arguments to the `ls` command.

Experiment further with `find`:

- `sudo find / -not -type l -perm -o+w`
- `sudo find / -perm -u+s -user root -type f`

Both of the above commands are useful for security auditing purposes. The first one searches for (non-symlink) world-writable files. The second one searches for files which are "setuid root," or in other words, run with root permissions by a non-root user.

#### Task 4:
Clean up:

- `cd ..`
- `rm -r lab44`

**Notes:**
Another useful command is `file`, which tells you a given file's type. Can you figure out how to use `file` in combination with find to locate all text files within your home directory?

## LAB 45

### Perform Basic File Management: Archiving and Unarchiving

**Lab Objective:**
Learn how to create, extract, and examine various types of archive files.

**Lab Purpose:**
In this lab, you will learn about gzip, bzip2, and xz compressed archives—as well as two tools, `tar` and `cpio`, to manage most Linux archive types.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

#### Task 1:
Open the Terminal application and run the following:

```bash
mkdir lab45
cd lab45
touch f1 f2 f3 f4 f5 f6 f7 f8 f9
```

#### Task 2:
Though ZIP is a common format and well-supported on Linux, it is not the main compression format Linux uses. That would be the classic gzip:

```bash
gzip f*
ls
```

Wait a minute... why are there now nine gzipped files instead of just one? And what happened to the originals?

This is why gzip is considered a *compression* format rather than an *archive* one. To create a single, easy-to-use archive file, we need a different tool...

#### Task 3:
Run: `tar -cf files.tar.gz f*`

Now, with the help of the tar archiver, you have your gzipped archive in files.tar.gz … well, sort of.

Normally, with a gzipped tarball, you would be able to extract it with `tar -xf files.tar.gz` and get all of the original files back. Instead, you could try that yourself now, and you would get the nine .gz files.

There's a better way. Let's blow this up and start over:

```bash
rm f*  
touch f1 f2 f3 f4 f5 f6 f7 f8 f9  
tar -czf archive.tar.gz f*  
tar --list -f archive.tar.gz
```

Ta-da! Now you see a list of nine files within your single compressed tarball.

#### Task 4:
gzip isn't the only format you can use with tar:

```bash
tar -cjf archive.tar.bz2 f*  
tar -cJf archive.tar.xz f*
```

The bzip2 and XZ formats, respectively, are newer and use different algorithms from gzip, but the end result is the same. tar can extract all of its formats in the same way, simply by using `tar -xf filename`.

#### Task 5:
cpio is another archiving tool used, most notably, in the RPM package manager and initramfs. Run:

- `find . | cpio -o > lab45.cpio`
- `cpio -t < lab45.cpio`
- `rm f1`
- `cpio -i -d f1 < lab45.cpio`
- `rm f*`
- `cpio -i -vd < lab45.cpio`

In short, what you are doing here is creating an archive, listing that archive (with -t), extracting the f1 file, and then extracting all of the files.

#### Task 6:
Another useful command for backups is `dd`. Typically this is used for block-level copying of an entire disk or partition, but it can also be used with ordinary files:

```bash
dd if=f1 of=f1.bak
```

Of course, if that's all you were doing, you could just use `cp`. A more typical usage would be something like (do not actually run this):

```bash
dd if=/dev/sda1 of=/dev/sdb1
```

Assuming you had already connected a backup drive, this would copy the entire /dev/sda1 partition onto it.

#### Task 7:
Finally, clean up:

```bash
cd ~
rm -r lab45
```

**Notes:**
To use compression-only without tar for archiving, each format has its own compression and decompression commands. Use gzip/gunzip, bzip2/bunzip2, and xz/unxz, for gzip, bzip2, and LZMA formats, respectively.

## LAB 46

### Use Streams, Pipes, and Redirects: Redirection and File Descriptors

**Lab Objective:**
Learn how to redirect input and output in Bash.

**Lab Purpose:**
Bash has a commonly-used feature, known as I/O redirection, that makes life easier when using Linux. In this lab, you will learn how to make use of this powerful feature.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

#### Task 1:
Open the Terminal application and run:

```bash
mkdir lab46
cd lab46
echo "hello world" > hello
cat hello
```

You just *redirected* the output from your `echo` command into the hello file. The `>` is a shortcut; the proper version of this would be `1>`, where `1` is called a *file descriptor*, which references the *standard output*.

#### Task 2:
Now run:

```bash
ls nonexistent 2>> hello
cat hello
```

Based on the new contents of the hello file ('ls: cannot access ‘nonexistent’: No such file or directory'), what can you surmise about the function of `2>>`? Here, 2 is a file descriptor for standard error.

#### Task 3:
Sometimes, you want to redirect both output and error to the same place. In ye olden days, you would have to do something ugly like this: `ls foo > bar 2>&1`

However, modern versions of Bash have an easy-to-use shortcut: `ls foo >& bar`

#### Task 4:
We've talked about redirecting output, but what about input? To learn about that, run the following commands:

```bash
cat < hello

read foo << "foo"
echo $foo

cat << END-OF-FILE > goodbye
hello
goodbye
END-OF-FILE
cat goodbye
```

In short: `<` redirects input from a file name, `<<` starts a here document, and `<<<` redirects input from another command.

#### Task 5:
You can also create your own file descriptors. Observe:

- `exec 3> foo`
- `echo "Hello World" >&3`
- `cat foo`
- `exec 3>&-`
- `echo "fail" >&3`

What this is doing is opening file descriptor 3 (for both reading and writing), with the file foo, and sending output to that. The fourth line then closes the file descriptor, causing the last echo command to fail.
