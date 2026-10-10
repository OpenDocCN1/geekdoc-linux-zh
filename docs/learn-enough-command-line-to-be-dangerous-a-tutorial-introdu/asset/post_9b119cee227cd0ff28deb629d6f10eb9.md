
The tilde character `~` (which is typed using Shift-backtick, located just to the left of the number 1 on most keyboards). As a result, the two paths shown in Figure 18 are identical: `/Users/mhart1/ruby/projects` is the same as `~/ruby/projects`. (Amusingly, the reason the tilde character is used for the home directory is simply because the "Home" key was the same as the key for producing "~" on *some early keyboards*.)

In addition to user directories, every Unix system has *system directories* for the programs essential for the computer's normal operation. Modifying system files or directories requires special powers granted only to the *superuser*, known as *root*. The superuser is so powerful that it's considered bad form to log in as *root*; instead, tasks executed as *root* should typically use the *sudo* command (Box 11).

### Box 11. "sudo make me a sandwich."

*sudo* gives ordinary users the power to execute commands as the superuser. For example, let's try *touch*ing a file in the system directory */opt* as follows:

```bash
$ touch /opt
touch: /opt/foo: Permission denied
```

Because normal users don't have permission to modify */opt*, the command fails, but it succeeds with *sudo*:

```bash
$ sudo touch /opt/foo
Password:
```

As shown, after entering *sudo* we are prompted to enter our user password; if entered correctly, and if the user has been configured to have *sudo* privileges (which is the default on most desktop Unix systems), then the command will succeed. As shown in Figure 19, this pattern of being denied at first, only to succeed using *sudo*, is a common theme in computing.

To check that the file really was created, we can *ls* it:

```bash
$ ls -l /opt/foo
-rw-r--r-- 1 root wheel 0 Jul 23 19:13 /opt/foo
```

Note that (1) a normal user can ls a file in a system directory (without sudo) and (2) the name root appears in the listing, indicating that the superuser owns the file. (The meaning of the second term, wheel, is a little obscure, but you can learn about it on a site called, appropriately enough, superuser.)

To remove the file we just created, we again need superuser status:

```bash
$ rm -f /opt/foo
rm: /opt/foo: Permission denied
$ sudo !!
$ !ls
ls: /opt/foo: No such file or directory
```

Here the first rm fails, so we've run sudo !!, which runs sudo and then the previous command, and we've followed that up with !ls, which runs the previous ls command (Box 9).

As a final comment, I'd like to note the English pronunciation of something like sudo !!, which is important when communicating via spoken language. As noted in Box 9, !! is pronounced “bang bang”. There is disagreement, though, on the pronunciation of sudo. Some people say “SOO-doh”, so that it sounds like the prefix pseudo, but in fact sudo is composed of the command su (which, contrary popular belief, stands for “substitute user” and not “superuser”) followed by the English word “do”. In other words, sudo is a contraction of “substitute user do”. Since (outside of solfege and The Sound of Music) the word “do” rhymes with “too”, the correct pronunciation of sudo is “SOO-doo”, and sudo !! would therefore be read as “SOO-doo bang bang”.

### Exercises

- 1. Write in words how you might speak the directory ~/foo/bar.

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_63_0.png)

Figure 19: “*Sandwich*” (via *xkcd.com*) derives humor from the behavior of *sudo*.

- 2. In `/Users/bill/sonnets`, what is the home directory? What is the username? Which directory is deepest in the hierarchy?
- 3. For a user with username `bill`, how do `/Users/bill/sonnets` and `~/sonnets` differ (if at all)?

### 4.2 Making directories

So far in this tutorial, we've created (and removed) a large number of text files. The time has finally come to make a directory to contain them. Although most modern operating systems include a graphical interface for this task, the Unix way to do it is with `mkdir` (short for “make directory”, per Figure 14):

```bash
$ mkdir text_files
```

Having made the directory, we can move the text files there using a wildcard:

```bash
$ mv *.txt text_files/
```

We can confirm the move worked by listing the directory:

```bash
$ ls text_files/
sonnet_1.txt    sonnet_1_reversed.txt   sonnets.txt
```

(Depending on how closely you've followed this tutorial, your results may vary.)

By default, running `ls` on a directory shows its *contents*, but we can show just the directory using the `-d` option:

```bash
$ ls -d text_files/
text_files
```

This usage is especially common with the `-l` option (Section 2.2):

```bash
$ ls -ld text_files/
drwxr-xr-x  7 mhartl staff  238 Jul 24 18:07 text_files
```

Finally, we can change directories using `cd`:

```bash
$ cd text_files/
```

Note that `cd` typically supports tab completion, so (as described in Box 8) we can actually type `cd tex<tab>`.

After running `cd`, we can confirm that we’re in the correct directory using the “print working directory” command, `pwd`, together with another call to `ls`:

```bash
$ pwd
/Users/mhart1/text_files
$ ls
sonnet_1.txt    sonnet_1_reversed.txt    sonnets.txt
```

These last steps of typing `pwd` to double-check the directory, and especially running `ls` to inspect the directory contents, are a matter of habit for many a grizzled command-line veteran. (Your result for `pwd` will, of course, be different, unless you happen to be using the username “mhart1” on OS X.)

### Exercises

- 1. What is the option for making intermediate directories as required, so that you can create, e.g., `~/foo` and `~/foo/bar` with a single command?
  - *Hint*: Refer to the man page for `mkdir`.
- 2. Use the option from the previous exercise to make the directory `foo` and, within it, the directory `bar` (i.e., `~/foo/bar`) with a single command.
- 3. By piping the output of `ls` to `grep`, list everything in the home directory that contains the letter “o”.

### 4.3 Navigating directories

We saw in Section 4.2 how to use `cd` to change to a directory with a given name. This is one of the most common ways of navigating, but there are a couple of special forms worth knowing. The first is changing to the directory one level up in the hierarchy using `cd ..` (read “see-dee dot-dot”):

```bash
$ pwd
/Users/mhart1/text_files
$ cd ..
$ pwd
/Users/mhart1
```

In this case, because `/Users/mhart1` is my *home directory*, we could have accomplished the same thing using `cd` by itself:

```bash
$ cd text_files/
$ pwd
/Users/mhart1/text_files
$ cd
$ pwd
/Users/mhart1
```

The reason this works is that `cd` by itself changes to the user’s home directory, wherever that is. This means that

```bash
$ cd
```

and

```bash
$ cd ~
```

are equivalent.

When changing directories, it’s frequently useful to be able to specify the home directory somehow. For example, suppose we make a second directory and `cd` into it:

```bash
$ pwd
/Users/mhart1
$ mkdir second_directory
$ cd second_directory/
```

Now if we want to change to the **text_files** directory, we can **cd** to **text_files** via the home directory `~`:

```bash
$ pwd
/Users/mhart1/second_directory
$ cd ~/text_files
$ pwd
/Users/mhart1/text_files
```

Incidentally, we’re now in a position to understand the prompts shown in Figure 6: I have my prompt configured to show the current directory, which might be things like `[~]`, `[ruby]`, or `[projects]`. (We’ll discuss how to customize the prompt in *Learn Enough™ Text Editor to Be Dangerous*. Especially eager (or impatient) readers can exercise their technical sophistication (Box 5) by Googling for *how to do it*.)

Closely related to `..` for “one directory up” is `.` (read “dot”) which means “the current directory”. The most common use of `.` is when moving or copying files to the current directory:

```bash
$ pwd
/Users/mhart1/text_files
$ cd ~/second_directory
$ ls
$ cp ~/text_files/sonnets.txt .
$ ls
sonnets.txt
```

Note in that the first call to `ls` returns nothing, because **second_directory** is initially empty.

Another common use of `.` is in conjunction with the **find** command, which like **grep** is insanely powerful, but in my own use it looks like this **99%** of the time:
