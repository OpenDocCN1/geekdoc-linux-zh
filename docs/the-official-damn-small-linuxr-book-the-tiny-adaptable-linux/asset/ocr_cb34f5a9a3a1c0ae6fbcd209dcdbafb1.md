+   - .uci type extensions are compressed loop images that are self-contained and mount under the /opt directory. All tar.gz extensions can easily be made into a uci type.
+   - .unc represents our latest extension type. Extensions of this type can only be used on later versions of DSL that support the unionfs file system. These extensions are compressed cloops that mounts into the base file system.

Don’t worry about fully understanding these extension types. Only know that both UCI and UNC are the preferred types. Both of these are mounted and therefore use considerably less system resources than the other two. Because these extension types are mounted, you can return your system to a pristine state by simply unmounting the extensions or rebooting. This is true no matter which type of the many installation types DSL offers is being used. You can save even more /ramdisk space by storing your UCI and UNC extensions on your hard disk or pen drive.

The tar.gz and .ds1 should really only be used if no other version of the extension is currently available and your system has the resources to support them. Because the tar.gz and .ds1 types copy all files from the extension file to separate locations in the file system, a low memory system can quickly run out of space in /ramdisk, as well as run out of inodes (one is consumed for each file and directory).

Now, let us continue with the normal procedure to use and enjoy the MyDSL system.

# Choosing and Getting Extensions

When you click one of the extension categories, an extension browser opens and displays a list of all available MyDSL packages in that category. For example, click the UCI category to see the list of UCI extensions shown in Figure 5-3.

![](bbox=[0.12, 0.81, 0.42, 0.95])

Clicking one of these packages displays its info file providing information about the extension. This includes the name and web address of the program’s creator, a brief description of the program, and any additional info that might be needed to