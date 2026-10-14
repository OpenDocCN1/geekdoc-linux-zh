configuration from the disk if it exists, and the latter confirms writing any LVM partitions you may have set up.

+   - **partman-auto/choose_recipe**  
+     The Ubuntu partition program allows a few different predefined partitioning recipes from which the user can choose. The atomic recipe sets up everything on a single partition. If you set the option to `home`, it will separate out a `/home` partition as well, and if you set it to `multi`, you will get separate `/home`, `/usr`, `/var`, and `/tmp` partitions.

+   - **partman/confirm_write_new_label, partman/choose_partition, and partman/confirm**  
+     These are more options that tell the installer to proceed with partitioning without extra user confirmation. If you did, however, want to require a user to confirm settings (possibly while debugging your preseed file), you could comment out one of these options.

**Expert Partition Recipes**  The predefined partition recipes that Ubuntu provides are probably adequate for basic servers, but most administrators I know have strong feelings about how their systems are partitioned. In these cases you will likely want to create your own custom partitioning scheme for your servers. In the preceding world this is known as an `expert_recipe`. Custom partitioning recipes can get rather complex as there are a lot of options available. The complete documentation is available at http://d-i.alioth.debian.org/svn/debian-installer/installer/doc/devel/partman-auto-recipe.txt, but even that can be difficult to follow without some examples.

First let’s examine a basic partitioning recipe that is provided in a lot of the example preseed files in official documentation. The following recipe will set up a small `/boot` partition and a swap partition and use up the rest of the disk for `/`:

```
d-i partman-auto/expert_recipe string                         \\
  boot-root ::                                               \\
    40 50 100 ext3                                           \\
            $primary{ } $bootable{ }                         \\
            method{ format }                                 \\
            use_filesystem{ } filesystem{ ext3 }             \\
            mountpoint{ /boot }                               \\
    .                                                         \\
```