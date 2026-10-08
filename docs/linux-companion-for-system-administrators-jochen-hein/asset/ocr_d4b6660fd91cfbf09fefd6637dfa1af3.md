# FILE SYSTEMS AND DATA MEDIA 115

group is full, you can add another physical volume and use the space. lvextend extends the size of a logical volume, and lvreduce reduces the size. See Listing 4.24 for an example. you can set the new size or enter the difference.

```
# lvextend -L256 /dev/rootvg/tmlv
lvextend -- extending logical volume "dev/rootvg/tmlv"
to 384 MB
lvextend -- doing automatic backup of volume group "rootvg"
lvextend -- logical volume "/dev/rootvg/tmplv"
successfully extended
zeus:(2):# lvreduce -L128 /dev/rootvg/tmplv
lvreduce -- reducing active volume of 256 MB
lvreduce -- THIS MAY DESTROY YOUR DATA
lvreduce -- do you really want to reduce "/dev/rootvg/tmplv"? Ey/
l]: y
lvreduce -- doing automatic backup of volume group "rootvg"
lvreduce -- logical volume "/dev/rootvg/tmplv"
successfully reduced
```

Listing 4.24 Resizing a logical volume.

This is not the complete truth. The device where the file system is stored now has no free space, but the file system is not aware of that space. You need programs that change the file system accordingly. There are two kinds of programs, online and offline programs. ext2resize is a offline-resizer. It is called with the device name and the new size of the file system (see Listing 4.25).

```
# ext2resize /dev/rootvg/tmplv 393216
ext2_resize_fs
ext22_grow_fs
extext2_block_relocate
...
```

Listing 4.25 Increasing the data files systems.

The program ef2fsadn is a frontend of lvextend and ext2resize, so you only need to enter a single command. Besides that, e2fsadn calls e2fsck first, so you start with a valid file system. There is also ext2online available, which can extend a file system that is currently in use. Until now you have had to apply a kernel patch before using that program. If you want to make