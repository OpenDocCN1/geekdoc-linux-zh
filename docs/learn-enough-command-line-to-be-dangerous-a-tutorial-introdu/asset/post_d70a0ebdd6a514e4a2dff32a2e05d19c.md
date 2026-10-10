
In words, what this does is find files whose names match the pattern `*.txt`, starting in the current directory `.` and then in its subdirectories. The find utility is incredibly useful for finding a misplaced file at the command line.

Perhaps my favorite use of `.` is in "open dot", which will work only on Macintosh OS X:

```bash
$ cd ~/ruby/projects
$ open .
```

The remarkable open command opens its argument using whatever the default program is for the given file or directory. (A similar command, xdg-open, works on some Linux systems.) For example, open foo.pdf would open the PDF file with the default viewer (which is Preview on most Macs). In the case of a directory such as `.`, that default program is the Finder, so open `.` produces a result like that shown in Figure 18.

A final navigational command, and one of my personal favorites, is `cd -` which cds to the previous directory, wherever it was:

```bash
$ pwd
/Users/mhartl/second_directory
$ cd ~/text_files
$ pwd
/Users/mhartl/text_file
$ cd -
/Users/mhartl/second_directory
```

I find that `cd -` is especially useful when combining commands, as described in Box 12.

> My directory has a huge number of text files, ‘cause that’s just how I roll, so the command I ran was really `find . -name '*.txt' | grep text_files`, which filters out anything that doesn’t match the directory being used in this tutorial.

## Box 12. Combining commands

It’s often convenient to combine commands at the command line, such as when installing software using the Unix programs configure and make, which often appear in the following sequence:

```bash
$ ./configure ; make ; make install
```

This line runs the configure program from the current directory `.`, and then runs both `make` and `make install`. (You are not expected to understand what these programs do, and indeed they won’t work on your system unless you happen to be in the directory of a program designed to be installed this way.) Because they are separated by the semicolon character `;`, three commands are run in sequence.

An even better way to combine commands is with the double-ampersand `&&`:

```bash
$ ./configure && make && make install
```

The difference is that commands separated by `&&` run only if the previous command succeeded. In contrast, with `;` all the commands will be run no matter what, which will cause an error in the likely case that subsequent commands depend on the results of the ones that precede them.

I especially like to use `&&` in combination with `cd -`, which lets me do things like this:

```bash
$ build_article && cd ~/tau && deploy && cd -
```

Again, you are not expected to understand these commands, but the general idea is that we can (say) build an article in one directory, `cd` to a different directory, deploy (perhaps a website) to production, and then `cd` back (`cd -`) to the original directory, where we can continue our work. Then, if need be, we can just use up arrow (or one of the techniques from Box 9) to retrieve the whole thing and do it all again.

## Exercises

- 1. How do the effects of `cd` and `cd ~` differ (or do they)?
- 2. Change to `text_directory`, then change to `second_directory` using the “one directory up” double dot operator `..`.
- 3. From wherever you are, create an empty file called `nil` in `text_directory` using whatever method you wish.
- 4. Remove `nil` from the previous exercises using a different path from the one you used before. (In other words, if you used the path `~/text_directory` before, use something like `../text_directory` or `/Users/<username>/text_directory`.)

### 4.4 Renaming, copying, and deleting directories

The commands for renaming, copying, and deleting directories are similar to those for files (Section 2.3), but there are some subtle differences worth noting. The command with the least difference is `mv`, which works just as it does for files:

```bash
$ mkdir foo
$ mv foo/ bar/
$ cd foo/
-bash: cd: foo: No such file or directory
$ cd bar/
```

Here the error message indicates that the `mv` worked: there is no file or directory called `foo`. (The word `bash` refers to the shell being run, in this case the “Bourne Again Shell”.) The only minor subtlety is that the trailing slashes (which are typically added automatically by tab completion (Box 8)) are optional:

```bash
$ cd
$ mv bar foo
$ cd foo/
```

This issue with trailing slashes never makes a difference with `mv`, but with `cp` it can be a source of much confusion. In particular, when copying directories, the behavior you usually want is to copy the directory contents *including* the directory, which on many systems requires leaving off the trailing slash. When copying files, you also need to include the `-r` option (for "recursive"). For example, to copy the contents of the `text_files` directory to a new directory called `foobar`, we use the command shown in Listing 17.

**Listing 17: Copying a directory.**

```bash
$ cd
$ mkdir foobar
$ cd foobar/
$ cp -r ../text_files .
$ ls
text_files
```

Note that we’ve used `..` to make a *relative path*, going up one directory and then into `text_files`. Also note the *lack* of a trailing slash in `cp -r ../text_files`; if we included it, we’d get Listing 18 instead.

**Listing 18: Copying with a trailing slash.**

```bash
$ cp -r ../text_files/ .
$ ls
sonnet_1.txt sonnet_1_reversed.txt sonnets.txt text_files
```

In other words, Listing 18 copies the individual files, but not the directory itself. As a result, I recommend always omitting the trailing slash, as in Listing 17; if you want to copy only the files, be explicit using the star operator, as in:

```bash
$ cp ../text_files/* .
```

Unlike renaming (moving) and copying directories, which use the same `mv` and `cp` commands used for files, in the case of removing directories there’s a dedicated command called `rmdir`. In my experience, though, it rarely works, as seen here:

```bash
$ cd
$ rmdir second_directory
rmdir: second_directory/: Directory not empty
```

The error message here is what happens 99% of the time when I try to remove directories, because `rmdir` requires the directory to be empty. You can of course empty it by hand (using `rm` repeatedly), but this is frequently inconvenient, and I almost always use the more powerful (but *much* more dangerous) “remove recursive force” command `rm -rf`, which removes a directory, its files, and any subdirectories without confirmation (Listing 19).

**Listing 19: Using `rm -rf` to remove a directory.**

```bash
$ rm -rf second_directory/
$ ls second_directory
ls: second_directory: No such file or directory
```

As the error message from `ls` in Listing 19 indicates (“No such file or directory”), our use of `rm -rf` succeeded in removing the directory.

The powerful command `rm -rf` is too convenient to ignore, but remember: “With great power comes great responsibility” (Figure 20).

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_73_0.png)

Figure 20: This *superhero* understands how to use the power of `rm -rf` responsibly.

## Grep redux

Now that we know a little about directories, we are in a position to add a useful `grep` variation to our toolkit from Section 3.4. As with `cp` and `rm`, `grep` takes a “recursive” option, `-r`, which in this case greps through a directory’s files and the files in its subdirectories. This is incredibly useful when you’re looking for a string in a file somewhere in a hierarchy of directories, but you’re not sure where the file is. Here’s the setup, which puts the word “*sesquipedalian*” in a file called `long_word.txt`:

```bash
$ cd text_files/
$ mkdir foo
$ cd foo/
$ echo sesquipedalian > long_word.txt
$ cd
```

The final `cd` puts us back in the home directory. Suppose we now want to find the file containing “sesquipedalian”. The way *not* to do it is this:

```bash
$ grep sesquipedalian text_files
grep: text_files: Is a directory
```

Here `grep`'s error message indicates that the command didn’t work, but adding `\-r` does the trick:

```bash
$ grep \-r sesquipedalian text_files
text_files/foo/long_word.txt:sesquipedalian
```

Because case rarely matters, I recommend making a habit of adding the `\-i` option when grepping recursively, as follows:

```bash
$ grep \-ri sesquipedalian text_files
text_files/foo/long_word.txt:sesquipedalian
```

Armed with `grep \-ri`, we are now equipped to find strings of our choice in arbitrarily deep hierarchies of directories.

## Exercises

- 1. Make a directory `foo` with a subdirectory `bar`, then rename the subdirectory to `baz`.
- 2. Copy all the files in `text_files`, *with* directory, into `foo`.
- 3. Copy all the files in `text_files`, *without* directory, into `bar`.
- 4. Remove `foo` and everything in it using a single command.

### 4.5 Summary

Important commands from this section are summarized in Table 5.
