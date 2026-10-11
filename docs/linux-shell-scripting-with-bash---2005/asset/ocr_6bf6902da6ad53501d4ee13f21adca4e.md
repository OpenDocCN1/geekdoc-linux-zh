Lines unaffected by `sed` can be hidden with the `~quiet` (or `~n` or `~silent`) switch.

Like the `transform` command, there are other `sed` commands that mimic Linux commands. The `p` (print) command imitates the `grep` command by printing a matching line. This is useful only when the `~quiet` switch is used. The `~` (line number) command prints the line number of matching lines. The `q` (quit) command makes `sed` act like the `head` command, displaying lines until a certain line is encountered.

```
$ head orders.txt | sed -quiet '/^$B/p'\
Bunk Bed,705.99,1,757\
Queen Bed,925.99,1,757\
\
$ head orders.txt | sed -quiet '/^$B/d'\
5\
6
```

The remaining `sed` commands represent specialized actions. The flow of control is handled by the `n` (next) command. Files can be read with `r` or written with `w`. `a` (append next) combines two lines into one for matching purposes. `d` (multiple line delete) deletes multiple lines. `p` is multiple line print. `h`, `H`, `g`, `G`, and `x` enable you to save lines to a temporary buffer so that you can make changes, display the results, and then restore the original text for further analysis. This works like an electronic calculator's memory. Complicated `sed` expressions can feature branches to labels embedded in the expressions using the `b` command. The `t` (test) command acts as a `shell if` or `switch` statement, attempting a series of operations until one succeeds. Subcommands can be embedded in `sed` with curly brackets. More documentation on these commands can be found using `info sed`.

Long `sed` scripts can be stored in a file. You can read the `sed` script from a file with the `~files` (or `~f`) switch. You can include comments with a `#` character, like a `shell` script.

`sed` expressions can also be specified using the `~expression` (or `~e`) switch, or can be read from standard input when a `~filename` is used.

You cannot use `ASCII` value escape sequences in `sed` patterns.

# ## Compressing Files

Most Linux programs differentiate between archiving and compression. *Archiving* is the storage of a number of files into a single file. *Compression* is a reduction of file size by encoding the file. In general, an archive file takes up more space than the original files, so most archive files are also compressed.

The Linux `bzip2` (BWH zip) command compresses files with Burrows–Wheeler–Huffman compression. This is the most commonly used compression format. Older compression programs are available on most distributions. `gzip` (GNU zip) compresses with `LZ77` compression and is used extensively on older distributions. `compress` is an older Lempel–Ziv compression program available on most versions of `Unix`. `zip` is the Linux version of the DOS `pkzip` program. `hexbin` decompresses certain Macintosh archives.