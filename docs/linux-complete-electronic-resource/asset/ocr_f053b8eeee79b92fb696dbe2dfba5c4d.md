an uppercase letter, the action applies to all files, and you won’t be prompted again.
You may also choose actions (for all files) on the command line, when invoking mtools:

+   -o    Overwrites primary names by default.
+   -O    Overwrites secondary names by default.
+   -r    Renames primary name by default.
+   -R    Renames secondary name by default.
+   -a    Autorenames primary name by default.
+   -A    Autorenames secondary name by default.
+   -s    Skip primary name by default.
+   -S    Skip secondary name by default.
+   -m    Ask user what to do with primary name.
+   -M    Ask user what to do with secondary name.

By default, the user is prompted if the primary name clashes, and the secondary name is auto-renamed.
If a name clash occurs in a Unix directory, mtools only asks whether to overwrite the file, or to skip it.

# CASE SENSITIVITY OF THE VFAT FILESYSTEM

The VFAT filesystem is able to remember the case of the filenames. However, filenames which differ only in case are not allowed to coexist in the same directory. For example if you store a file called LongFileName on a VFAT filesystem, mdir shows this file as LongFileName, and not as Longfilename. However, if you then try to add LongFilename to the same directory, it is refused, because case is ignored for clash checks.

The VFAT filesystem allows you to store the case of a filename in the attribute byte, if all letters of the filename are the same case, and if all letters of the extension are the same case too. Mtools uses this information when displaying the files, and also to generate the Unix filename when copying to a Unix directory. This may have unexpected results when applied to files written using an pre-7 version of DOS: Indeed, the old style filenames map to all uppercase. This is different from the behavior of the old version of mtools which used to generate lowercase Unix filenames.