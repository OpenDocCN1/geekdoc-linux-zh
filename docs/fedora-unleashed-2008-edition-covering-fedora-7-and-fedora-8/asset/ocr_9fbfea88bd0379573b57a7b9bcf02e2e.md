symlink is pointing at. The fact that symlinks are really just dumb pointers has two advantages: You can link to something that does not exist (and create it later if you want), and you can link to directories.

Both types of links have their uses. Creating a hard link is a great way to back up a file on the same disk. For example, if you delete the file in one location, it still exists untouched in the other location. Symlinks are popular because they allow a file to appear to be in a different location; you could store your website in `/var/www/live` and an under-construction holding page in `/var/www/construction`. Then you could have Apache point to a symlink `/var/www/html` that is redirected to either the live or construction directory depending on what you need.

> TIP
> The shred command overwrites a file’s contents with random data, allowing for safe deletion. Because this directly affects a file’s contents, rather than just a filename, this means that all filenames hard linked to an inoide are affected.

Both types of link are created with the `ln` command. By default, the `ln` command creates hard links, but you can create symlinks by passing it the `-s` parameter. The syntax is `ln [-s] <something> <somewhere>`, for example:

```
$ ln -s myfile.txt mylink
```

That command creates the symlink `mylink` that points to `myfile.txt`. Remove the `-s` to create a hard link. You can verify that your link has been created by running `ls -l`. Your symlink should look something like this:

```
lrwxrwxrwx  1 paul paul     5 2007-11-12 12:39 mylink -> myfile.txt
```

Note how the file properties start with l (lowercase L) for link and how `ls -l` also prints where the link is going. Symlinks are always very small in size; the previous link is 5 bytes in size. If you created a hard link, it should look like this:

```
-rw-rw-r--  2 paul paul    341 2007-11-12 12:39 mylink
```

This time the file has normal attributes, but the second number is 2 rather than 1. That number is how many hard links point to this file, which is why it is 2 now. The file size is also the same as that of the previous filename because it is the file, as opposed to just being a pointer.

Symlinks are used extensively in Linux. Programs that have been superseded, such as `sh`, now point to their replacements (in this case, `bash`), and library versioning is accomplished through symlinks. For example, applications that link against `zlib` load `/usr/lib/libz.so`. Internally, however, that is just a symlink that points to the actual `zlib` library: `/usr/lib/libz.so.1.2.1.2`. This enables multiple versions of libraries to be installed without applications needing to worry about the version name.