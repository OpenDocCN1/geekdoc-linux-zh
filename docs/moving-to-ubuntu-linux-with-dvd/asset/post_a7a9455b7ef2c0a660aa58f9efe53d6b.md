
just below or (depending on the keyboard) just above the Enter key and sharing space with the backslash key. Here's how it works:

```
cat random_names | sort | wc -w > num_names
```

In the preceding example, the output from the `cat` command is piped into `sort`, whose output is then piped into the `wc` command (that's *word count*). The `-w` flag tells `wc` to count the number of words in `random_names`. So far, so good.

That `cat` at the beginning is actually redundant, but I want to stack up a few commands for you to give you an idea of the power of piping. Ordinarily, I would write that command as follows:

```
sort random_names | wc -w > num_names
```

The `cat` is extraneous because `sort` incorporates its function. Using pipes is a great timesaver because you don't always need to have output at every step of the way.

### tee: A Very Special Pipe

Suppose that you want to send the output of a command to another command, but you also want to see the results at some point. Using the previous word count example, if you want a sorted list of names, but you also want the word count, you might have to use two different commands: one to generate the sorted list and another to count the number of words. Wouldn't it be nice if you could direct part of the output one way and have the rest continue in another direction? For this, use the `tee` command.

```
sort random_names | tee sorted_list | wc -w > num_names
```

The output from `sort` is now sitting in a file called `sorted_list`, whereas the rest of the output continues on to `wc` for a word count.

### STDERR

What about `STDERR`? Some commands (many, in fact) treat the error output differently than the `STDOUT`. If you are running the command at your terminal and that's all you want, there is no problem. Sometimes, though, the output is quite wordy and you need to capture it and look at it later. Unfortunately, using the STDOUT redirect (the greater-than sign) is only going to be so useful. Error messages that are generated (such as warning messages from a compilation) go to the terminal as before. One way to deal with this is to start by redirecting STDERR to STDOUT, and then redirect that to a file. Here's the line I use for this:

```
command_name 2>&1 > logfile.out
```

Remember that file descriptor 2 is STDERR and that file descriptor 1 is STDOUT. That's what that 2>&1 construct is all about. You are redirecting fd2 to fd1 and then redirecting that output to the file of your choice. Using that program compilation example, you might wind up with something like this:

```
make -f Makefile.linux 2>&1 > compilation.output
```

> **Quick Tip** The final greater-than sign in the preceding example could be eliminated completely. When using the 2>&1 construct, it is assumed that what follows is a filename.

## The Road to Nowhere

If the command happens to be verbose by nature and doesn't have a quiet switch, you can redirect that STDOUT and STDERR noise to what longtime Linux users like to call the *bit bucket*, a special file called `/dev/null`—literally, a road to nowhere. Anything fed to the bit bucket takes up no space and is never seen or heard from again. When I was in school, we would tell people to shut up by saying, "Dev null it, will you?" As you can see, we were easily amused.

To redirect output to the bit bucket, use the STDOUT redirection.

```
command -option > /dev/null
```

If, for some strange reason, you want to sort the output of the random_names files and you do not want to see the output, you can redirect the whole thing to /dev/null in this way:

```
sort random_names > /dev/null
```

Using the program compilation example where you had separate STDOUT and STDERR streams, you can combine the output to the bit bucket.

```
make -f makefile.linux 2>&1 /dev/null
```

That's actually a crazy example because you do want to see what goes on, but redirecting both STDOUT and STDERR to /dev/null is quite common when dealing with automated processes running in the background.

## Linux Commands: Working with Directories

There is another batch of commands suited to working with directory files (directories being just another type of file).

- `pwd`: Print Working Directory
- `cd`: Change to a new Directory
- `mkdir`: Make or create a new Directory
- `mv`: Move directories, or files, and rename them
- `rmdir`: Remove or delete Directories

One way to create a complicated directory structure is to use the mkdir command to create each and every directory.

```
mkdir /dir1
mkdir /dir1/sub_dir
mkdir /dir1/sub_dir/yetanotherdir
```

You could save yourself a few keystrokes and use the -p flag. This tells mkdir to create any parent directories that might not already exist. If you happen to like a lot of verborage from your system, you could also add the --verbose flag for good measure.

```
mkdir -p /dir1/sub_dir/yetanoherdir
```

To rename or move a directory, the format is the same as you used with a file or group of files. Use the mv command.

```
mv path_to_dir new_path_to_dir
```

Removing a directory can be a bit more challenging. The command `rmdir` seems simple enough. In fact, removing this directory was no problem:

```
$ rmdir trivia_dir
```

Removing this one, however, gave me an error:

```
$ rmdir junk_dir
rmdir: junk_dir: Directory not empty
```

You can only use `rmdir` to remove an empty directory. There is a -p option (as in *parents*) that enables you to remove a directory structure. For instance, you could remove a couple of levels like this:

```
rmdir -p junk_dir/level1/level2/level3
```

> **Warning** Beware of the `rm -rf *` command. Better yet, never use it. If you must delete an entire directory structure, change the directory to the one above it and explicitly remove the directory. This is also the first and best reason to do as much of your work as possible as a normal user and not root. Because root is all powerful, it is quite capable of completely destroying your system. Imagine that you are in the top-level directory ( / ) instead of /home/myname/junkdir when you initiate that recursive delete. It is far too easy to make this kind of mistake. *Beware.*

All the directories from `junk_dir` on down are removed, but *only* if they are empty of files. A better approach is to use the `rm` command with the -r, or *recursive*, option. Unless you are deleting only a couple of files or directories, you want to use the -f option as well.

```
$ rm -rf junk_dir
```

## There’s No Place Like $HOME

Yeah, I know. It’s a pretty cheesy pun, but I like it.

Because you’ve had a chance to play with a few directory commands, I’d like to take a moment and talk about a very special directory. Every user on your system has a home directory. That directory can be referenced with the $HOME environment variable. To get back to your home directory at any time, simply type `cd $HOME` and no matter where you were, there you are. Actually, you only need to type `cd`, press <Enter>, and you are home. The $HOME is implied.

The $HOME shortcut is great for shell scripts or anytime you want to save yourself some keystrokes. For instance, say you want to copy the file `remote.file` to your home directory and you are sitting in /usr/some_remote/dir. You could use either of the next two commands:

```
cp remote.file /home/my_username
cp remote.file $HOME
```

The second command saves you keystrokes, and the more time you spend doing system administration, the more you will love shortcuts like this. To save the maximum keystrokes, you can also use the tilde (~), a special character synonym for $HOME.

```
cp remote.file ~
```

## More on File Permissions

What you can and can’t do with a file, as defined by your username or group name, is pretty much wrapped up in four little letters. Look at the following listing (using `ls -l`) for an example. The permissions are at the beginning of each line.

```
-rw-r--r--  1 mgagne mgagne     937 May 17 13:22 conf_details
-rwxr-xr-x  1 root   root   45916220 Apr  4 12:25 gimp
-rw-r--r--  1 root   root     826 Feb 12 09:43 mail_test
-rw-r--r--  1 mgagne mgagne   44595 May 17 13:22 sk_open.jpg
```
