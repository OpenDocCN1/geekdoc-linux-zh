# **TABLE 2.3** Common `ln` Options

| Option Name | Option Abbreviation | Meaning |
| :--- | :--- | :--- |
| `--force` | `-f` | This option causes `ln` to remove any existing links or files that have the target *link* name. |
| `--directory` | `-d` or `-F` | Ordinarily, you can't create hard links to directories. The root user can attempt to do so, though, by passing this option to `ln`. (Symbolic links to directories are not a problem. This distinction is described shortly.) In practice, this option is unlikely to work, since few filesystems support hard links to directories. |
| `--symlink` | `-s` | The `ln` command creates hard links by default. To create a symbolic link, pass this option to the command. |

A few other options exist to perform more obscure tasks; consult the `ln` man page for details. The default type of link created by `ln`, hard links, are produced by creating two directory entries that point to the same file. Both filenames are equally valid and prominent; neither is a “truer” filename than the other, except that one was created first (when creating the file) and the other was created second. To delete the file, you must delete both hard links to the file. Because of the way hard links are created, all the links to a single file must exist on one low-level filesystem; you can’t create a hard link from, say, your root (/) filesystem to a separate filesystem you’ve mounted on it, such as your /home filesystem (if it’s on a separate partition). The underlying filesystem must support hard links. All Linux native filesystems support this feature, but some non-Linux filesystems don’t.

Symbolic links, by contrast, are special file types. The symbolic link is a separate file whose contents point to the linked-to file. Linux knows to access the linked-to file when you try to access the symbolic link, so in most respects accessing a symbolic link works just like accessing the original file. Because symbolic links are basically files that contain filenames, they can point across low-level filesystems—you can point from the root (/) filesystem to a file on a separate /home filesystem, for instance. The lookup process for accessing the original file from the link consumes a tiny bit of time, so symbolic link access is slower than hard link access—but not by enough that you’d notice in any but very bizarre conditions or artificial tests. Long directory listings show the linked-to file:

```
$ ls -l alink.odt
lrwxrwxrwx 1 rosmith users 8 Dec 2 15:31 alink.odt -> test.odt
```