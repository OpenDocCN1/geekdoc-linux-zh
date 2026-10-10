![](bbox=[0.43, 0.07, 0.61, 0.21])

Figure 12.2
BeagleBone kernel structure.

Finally, we need to get a power management firmware file from another source:

+   * wget http://arago-project.org/git/projects/?p=am33x-cm3.git\;a=blob_plain\;f=bin/
+   am335x-pm-firmware.bin\;hb=HEAD -O kernel/firmware/am335x-pm-firmware.bin

# ### Patching the Kernel

The mechanism for changing released source code in an orderly manner is the patch utility. The input to patch is a text file created by the diff utility that compares two files and reports any differences. So, when an Open Source programmer wants to distribute an upgrade to released source code, she does a diff between the modified code and the original code, redirecting the output of diff to a patch file. Something like this:

```
diff -uNPR original_code new_code > file.patch
```

The .patch extension is not required, but is the convention. See the diff man page to learn what the various options represent.

Then, to apply the patch, copy the patch file to the directory containing the original code and execute:

```
patch -p1 < file.patch
```

Note that patch diff normally takes its input from stdin, so we have to redirect input to the file. The -p1 flag tells patch to remove one slash and everything before it from the names of files to be patched. This recognizes the usual situation that the root directory from which the patch was created is not the same as the directory in which we are applying it. Removing everything in the path before the first slash makes the directories relative.

You could have diff create one gigantic patch file for the entire kernel source tree. The BeagleBone developers chose not to do that, opting instead to create individual patches for each file that is modified. This adds up to over a 1000 files in the patches/ subdirectory. The motivation for this is that it is probably easier to distribute updates to individual files.