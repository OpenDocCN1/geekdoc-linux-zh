# ## Examining and Manipulating Compressed Files with zcat

The next command, `zcat`, is used for two reasons:

+   - To examine the contents of a compressed file without going through the process of uncompressing it
+   - To use a compressed file as input to one or more piped commands

We use `zcat` for the first purpose in Example 9.17. The output from `zcat` is the same as the output of the uncompressed file, similar to what you would get with `cat`. You can see that `zcat` does the same thing for compressed files that its counterpart `cat` does for uncompressed files. Like `cat`, `zcat` cannot go back and forth through the file output. For this purpose, you might want to use the `zless` command, which behaves just like the `less` program (see Chapter 5, “Using Files in Linux,” to review the `less` command) except that it requires compressed files as input arguments. The syntax for `zcat` is

```
$ `zcat [-options] filename(s)<Enter>`
```

# **Example 9.17 Examining Compressed File Contents with zcat**

After Juana has combined the telephone list files into one and then compressed that one file (see Example 9.16), she wants to check that the compressed file is in good shape as far as content and format before she transmits it to La Mancha. She uses `zcat`, piped to `less`, to do so:

```
$ `zcat RFI_Phone$.gz | less<Enter>`
```

`zcat` responds with an output similar to the one she would have received if she had used `cat` on the original uncompressed file.

# ## Uncompressing Files with gunzip

The `gunzip` command uncompresses files that have been compressed with `gzip` or `compress`. Basically, `gunzip` reverses the `gzip` process, restoring the compressed file to its original uncompressed components. Its syntax is as follows:

```
$ `gunzip [-options] filename(s)<Enter>`
```