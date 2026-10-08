# patch

For all path names in the patch file that indicate the names of files to be patched, delete .num path-name components from the beginning of each path name. If the path name in the patch file is absolute, consider any leading slashes as the first component (that is, -p removes the leading slashes). Specifying -p uses the full path name. If you do not specify -p, use only the basename (the final path-name component).

-p num

Reverse the sense of the patch script, that is, assume that the script was created from the new version to the old version. You cannot use the -R option with ed scripts; patch tries to reverse each portion of the script before applying it. Save rejected differences in swapped format. If you do not specify this option and until a portion of the patch file is successfully applied, patch tries to apply each portion in its reversed sense as well as in its normal sense. If the attempt is successful, prompt the user to determine if the -R option should be set.

-R

-r rejectfile

Interpret the patch file as a unified context difference, that is, the output of the diff command when the -u or -U option is specified. New in the Solaris 9 release.

-u

# Operands

file

A path name of a file to patch.

# Usage

- -R option does not work with ed scripts because there is too little information to reconstruct the reverse operation.
The -p option makes it possible to customize a patchfile to local directory structures without manually editing the patchfile. For example, if the path name in the patch file was /curds/whey/src/blurfl/blurfl.c

setting -p 0 results in the same path name unmodified. Setting -p 1 returns the following path.
curds/whey/src/blurfl/blurfl.c

Without the leading slash, -p 4 returns the following path.
blurfl/blurfl.c

Not specifying -p at all returns the following path.
blurfl.c.

When using -b in some file-system implementations, the saving of a .orig file can produce unwanted results. With 12-, 13- or 14-character file names on file systems supporting 14-character maximum file names, the .orig file overwrites the new file.

![](bbox=[0.843, 0.453, 0.943, 0.493])