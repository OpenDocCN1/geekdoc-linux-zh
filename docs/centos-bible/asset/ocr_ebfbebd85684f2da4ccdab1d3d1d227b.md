output, you should see read and write speeds supported by the drive. Note that those are maximum possible speeds, so the actual maximum write speeds will depend on the CD or DVD media you are using.

The procedure for writing to DVDIs is almost identical to backing up data onto a CD disk, with the following exceptions:

+   - Each backup disk can hold a lot more data (4.7 GB for single-layer and 8.5 GB for dual-layer DVD, as compared to 700 MB for CDs).
+   
+   - Both the DVD writer and medium are more expensive than the CD counterparts, although the cost of DVD writers has come down drastically in the past few years.

> **NOTE** When manufacturers say 4.7 GB, they are talking about 1,000 MB per GB, not 1,024 MB. Therefore, you can really only store up to about 4.3 GB of data on a DVD (or, more precisely, 4,294,967,296 bytes).

There are also a few other issues you should be aware of that relate to using DVD media to record from Linux:

+   - While most new writable DVD drives today support both DVD-R and DVD+R formats, some older drives may not support DVD+R.
+   
+   - DVD+RW media that have not been formatted must be formatted before you can write to them. However, you can use `cdrecord` on an unformatted DVD+RW because it will automatically detect and format an unformatted disk. To force a format, you can use the `-format` option to `cdrecord`. There is also a `dvd+rw-format` that you can use to format a DVD drive (just run `dvd+rw-format` with your DVD device as the option).
+   
+   - You don't need to reformat DVD-RW media more than once. Multiple reformats can make the DVD-RW media unusable.

Follow the procedure in the "Writable CD Drives" section to create a file system image file (using `mkisofs`) and determine the location of your DVD-R driver. Then use the `cdrecord` command to actually burn the DVD. Here is an example of a `cdrecord` command line that burns a file system image called `bigimage.iso`:

```
`# cdrecord -v speed=2 dev=/dev/cdrom -data bigimage.iso`
```

# ## Writing CDs or DVDs with `growisofs`

Instead of doing separate `mkisofs` and `cdrecord` commands, as just shown, you can use the `growisofs` command to combine the function of those two commands. The `growisofs` command is particularly useful for mastering of large ISO images (such as those for double-layer DVD recording). That's because instead of copying the ISO image you create to a file (as `mkisofs` does), `growisofs` sends the ISO image directly to the CD or DVD to be burned.