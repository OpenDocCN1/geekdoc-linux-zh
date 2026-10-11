Here are the resulting commands:

```
echo "Patch @0:"
patch -p0 -s < /usr/src/redhat/SOURCES/patch-zero
```

The `%patch` macro nicely displays a message showing that a patch is being applied, and then invokes the `patch` command to actually do the dirty work. There are two options to the `patch` command:

+   - The `-p` option, which directs `patch` to remove the specified number of slashes (and any intervening directories) from the front of any filenames specified in the patch file. In this case, nothing will be removed.
+   - The `-s` option, which directs `patch` to apply the patch without displaying any informational messages. Only errors from `patch` will be displayed.

How did the `%patch` macro know which patch to apply? Keep in mind that, like the source tag lines, every patch tag is numbered, starting at `0`. The `%patch` macro, by default, applies the patch file named on the `patch` (or `patch0`) tag line.

# 13.4.2.1. Specifying Which patch Tag to Use

The `%patch` macro actually has two different ways to specify the `patch` tag line it is to use. The first method is to simply append the number of the desired `patch` tag to the end of the `%patch` macro itself. For example, in order to apply the patch specified on the `patch2` tag line, the following `%patch` macro could be used:

```
%patch2
```

The other approach is to use the `-P` option. This option is followed by the number of the `patch` tag line desired. Therefore, this line is identical in function to the previous one:

```
%patch -P 2
```

Note that the `-P` option will not apply the file specified on the `patch0` line, by default. Therefore, if you choose to use the `-P` option to specify `patch` numbers, you'll need to use the following format when applying patch `0`:

```
%patch -P 0
```

# 13.4.2.2. -p <#>: Strip <> Leading Slashes and Directories from patch Filenames

The `-p` (note the lowercase `p`) option is sent directly to the `patch` command. It is followed by a number, which specifies the number of leading slashes (and the directories in between) to strip from any filenames present in the patch file. For more information on this option, consult the `patch` man page.