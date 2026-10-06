# # Managing Links

In Linux, a link is a way to give file multiple identities, similar to shortcuts in Windows and aliases in Mac OS. Linux employs links to help make files more accessible, give commands multiple names, enable programs that look for the files in different locations to access the files, and so on. Two types of links exist: hard links and symbolic links (aka soft links). (Their differences are described in more detail shortly.) The ln command creates links. Its syntax is similar to that of cp:

```
ln [options] source link
```

The source is the original file, and the link is the name of the link you want to create. This command supports options and has several effects:

**Remove Target Files** The -f force option ln to remove existing links or files that have the target name. The -i or --interactive option has a similar effect, but it queries before replacing existing links

**Create Directory Hard Links** Ordinarily, you can't create hard links to directories. The root user can attempt to do so, by passing the -d, -F, or --directory option to ln. (Symbolic links to directories aren't a problem.) In practice, this feature is unlikely to work because most systems don't support it.

**Create a Symbolic Link** The ln command creates hard links by default. To create a symbolic link, use the -s or --symbolic option to the command.

A other options exist to perform more obscure tasks; consult ln's page for details.

By default, ln creates hard links, which are produced by creating two directory entries that point to the same file (precisely the same inode). Both filenames are valid and prominent; one is a "truer" filename than the other, except that one was created first (when creating the file) and the other was created second. To delete the file, you must delete both hard links to the file. Because of the way hard links work, they must exist on a single low-level filesystem; you can't create a hard link from say, your root (/) filesystem to a separate filesystem you've mounted, such as /home (if it is a separate filesystem). The underlying filesystem must support hard links. All Linux-native filesystems support this feature, but non-Linux filesystems don't.

Symbolic links, by contrast, are special types. The symbolic link is a separate file whose contents point to the linked-to file when you try to access the symbolic link, so in most respects accessing a symbolic link works just like accessing the original file. Because symbolic links are basically files that contain filenames, they can point across low-level filesystems—you can point from the root (/) filesystem to a file on a separate /home filesystem, instance. The lookup process for accessing the original file from the link consumes a bit of time, so symbolic link access is slower than hard link access—but not enough that you'd notice in any but very bizarre conditions or artificial tests. Long directory listings shows the linked-to file: