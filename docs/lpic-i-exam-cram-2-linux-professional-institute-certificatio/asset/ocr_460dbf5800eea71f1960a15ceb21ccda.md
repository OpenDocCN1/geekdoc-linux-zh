```
```
. . . dir1
├─┬─ file1
└─┬─ subdir1
```
```

The correct way to copy the contents of `dir1` into `dir2`, thereby mirroring `dir1` exactly, is to focus on the word *contents*. By suffixing the source (`dir1`) with a forward slash and an asterisk (`dir1/*`), you tell the `cp` command to ignore the directory entry and act only on the contents of that directory.

With the same initial setup, if you issue the command `cp -r dir1/* dir2`, you’ll get the correct results:

```
```
. . . dir1
├─┬─ file1
└─┬─ subdir1
. . . dir2
├─┬─ file1
└─┬─ subdir1
```
```

> > **ALERT!** The inability to properly copy a directory or its contents will come back to haunt you on the exam. In addition, if you see a source directory with only a trailing forward slash (`dir1/`) but no asterisk, it’s identical to using (`dir1`). In other words, to copy just the contents of a directory, you have to address them specifically with the forward slash and asterisk (`dir1/*`).

Another interesting use of the path and the single and double dot (`. and `..`) characters in each directory is to copy something from an existing directory or set of files to your current location.

For example, if you are currently in the `/home/rossb` directory and want to copy a set of files from the `/home/lukec` directory, you can avoid typing the full path of the current directory with the (`.`) character. Both of these commands perform the same action :

```
```
cp /home/lukec/*.mp3 .
cp /home/lukec/* .mp3 /home/rossb
```
```

# ## Moving Objects

Where the `cp` command copies a file and creates a new file system entry, inode, and data, the `mv` command simply changes which directory file contains the file or directory entry or alters the entry in the file if it stays in the same directory.

Create a file named `file1`; then run the `stat` command on it to check the details, like so:

```
```
touch file1
stat file1
     File: 'file1'
```
```