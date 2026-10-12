rather than to create an archive of them. You can use the `tar`, `cp`, `rsync`, or even the `cpio` commands to do this, as well as a handy file management tool known as `mc`. Using `tar` is the traditional choice because older versions of `cp` did not handle symbolic links and permissions well at times, causing those attributes (characteristics of the file) to be lost; `tar` handled those file attributes in a better manner. `cp` has been improved to fix those problems, but `tar` is still more widely used. `rsync` has recently been added to Fedora Core and is an excellent choice for mirroring sets of files, especially when done over a network.

Many choices exist for using file copying as a backup technique, and your choice will depend on your priorities. If you are interested in the simplest method, choose `cp -a`. The `tar` alternative is the next best option. `cpio` is better suited to creating archives than it is to simply copying files. `mc` might offer the best combination of ease, power, and flexibility, but it cannot be counted on to be found on every system; you should find `tar` and `cp` everywhere. The following sections describe how to use each of these methods so that you can better determine which is best for your situation.

To illustrate how to use file copying as a backup technique, the examples here show how to copy (not archive) a directory tree. This tree includes symbolic links and files that have special file permissions we need to keep intact.

# ## Copying Files Using tar

One choice for copying files into another location would be to use the `tar` command where you would create a `tar` file that would be piped to `tar` to be uncompressed in the new location. To accomplish this, first change to the source directory. Then, the entire command resembles

```
```
# tar cvf - files | ( cd target_directory ; tar xpf - )
```
```

where `files` are the filenames you want to include; use `*` to include the entire current directory.

Here is how the command shown works: You have already changed to the source directory and executed `tar` with the `cvf -` arguments that tell `tar` to

+   - `c`—Create an archive.
+   - `v`—Verbose; lists the files processed so we can see that it is working.
+   - `f`—The filename of the archive will be what follows. (In this case, it is -.)
+   - `--`—A buffer; a place to hold our data temporarily.

The following `tar` commands can be useful for creating file copies for backup purposes:

+   - `l`—Stay in the local file system (so you do not include remote volumes).
+   - `time-preserve`—Do not change access times on files, even though you are accessing them now, to preserve the old access information for archival purposes.