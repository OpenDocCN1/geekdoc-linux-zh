# OPTIONS

<patch>...

The files to read the patch from. - can be used to read from the standard input.

+   —stat

Instead of applying the patch, output diffstat for the input. Turns off “apply”.

+   —numstat

Similar to —stat, but shows the number of added and deleted lines in decimal notation and the pathname without abbreviation, to make it more machine friendly. For binary files, outputs two - instead of saying 0 0. Turns off “apply”.

+   —summary

Instead of applying the patch, output a condensed summary of information obtained from git diff extended headers, such as creations, renames and mode changes. Turns off “apply”.

+   —check

Instead of applying the patch, see if the patch is applicable to the current working tree and/or the index file and detects errors. Turns off “apply”.

+   —index

When —check is in effect, or when applying the patch (which is the default when none of the options that disables it is in effect), make sure the patch is applicable to what the current index file records. If the file to be patched in the working tree is not up-to-date, it is flagged as an error. This flag also causes the index file to be updated.

+   —cached

Apply a patch without touching the working tree. Instead take the cached data, apply the patch, and store the result in the index without using the working tree. This implies —index.

+   -3, —3way

When the patch does not apply cleanly, fall back on 3-way merge if the patch records the identity of blobs it is supposed to apply to, and we have those blobs available locally, possibly leaving the conflict markers in the files in the working tree for the user to resolve. This option implies the —index option, and is incompatible with the