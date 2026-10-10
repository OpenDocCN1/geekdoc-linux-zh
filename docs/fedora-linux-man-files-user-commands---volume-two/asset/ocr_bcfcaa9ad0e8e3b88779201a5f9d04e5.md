# ## NOTES

**genisoimage** may safely be installed **suid root**. This may be needed to allow **genisoimage** to read the previous session when creating a multisession image.

If **genisoimage** is creating a filesystem image with Rock Ridge attributes and the directory nesting level of the source directory tree is too much for ISO9660, **genisoimage** will do deep directory relocation. This results in a directory called **RR_MOVED** in the root directory of the CD. You cannot avoid this directory.

Many boot code options for different platforms are mutually exclusive because the boot blocks cannot coexist, ie. different platforms share the same data locations in the image. See for details.