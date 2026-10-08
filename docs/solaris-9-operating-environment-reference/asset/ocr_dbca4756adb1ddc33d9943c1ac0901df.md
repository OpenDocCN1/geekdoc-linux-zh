1022

patch

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of patch: LC_CTYPE, LC_MESSAGES, LC_TIME, and NLSPATH.

# Output Files

The output of patching the save files (.orig suffixes) and the reject files (.rej suffixes) is text files.

# Extended Description

A patchfile can contain patching instructions for more than one file. When you specify the -b-option, for each patched file, the original is saved in a file of the same name with the suffix .orig appended to it.

For each patched file, a reject file can also be created, and noted in "Patch Application" on page 1023. In the absence of a -r -option, the name of this file is formed by appending the suffix .rej to the original file name.

# Patch-file Format

The patch file must contain zero or more lines of header information followed by one or more patches. Each patch must contain zero or more lines of file-name identification in the format produced by diff -c and one or more sets of diff out, which are commonly called hunks.

patch recognizes the following expression in the header information.

Index: pathname The file to be patched is named pathname.

If all lines (including headers) within a patch begin with the same sequence of blank characters, patch removes this sequence before proceeding. Within each patch, if the type of difference is context, patch recognizes the following expressions.

+   *** filename timestamp The patches arise from filename.
*** filename timestamp The patches should be applied to filename.

Each hunk within a patch must be the diff output to change a line range within the original file. The line numbers for successive hunks within a patch must occur in ascending order.

# File-name Determination

If you specify no operand, patch performs the following steps to obtain a path name.

+   1. If the patch contains the strings *** and ---, patch strips components from the beginning of each patch name (depending on the presence or value of the -p-option) and tests for the existence of both files in the current directory (or directory specified with the -d option).
2. If both files exist, patch assumes that no path name can be obtained from this step. If the header information contains a line with the string Index:, patch strips components from the beginning of the path name (depending on -p) and then tests for the existence of this file in the current directory (or directory specified with the -d option).
3. If an an SCCS exists in the current directory, patch tries to perform a get -e SCCS/.filename to retrieve an editable version of the file.