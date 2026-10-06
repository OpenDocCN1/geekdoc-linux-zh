# diff

Displays the differences between two files
diff [options] file1 file2
diff [options] file1 directory
diff [options] directory file2
diff [options] directory1 directory

The diff utility displays line-by-line differences between two files. By default diff displays the differ-
ences as instructions that you can use to edit one of the files to make it the same as the other.

# Arguments

The file1 and file2 are pathnames of the files that diff works on. When the directory ar-
gument is used in place of file2, diff looks for a file in directory2 with the same name as
file1. Similarly, when the directory argument is used of file1, diff looks for a
file in directory1 with the same name as file2. You can use a hyphen in place of file1 or
file2 to cause diff to use standard input. When you specify two directory arguments,
diff compares all the files in directory1 with the files that have the same simple file-names in directory2.

# Options

+   --brief -q Does not display the differences between lines in the files. Instead, diff reports
only that the files differ.
--context [lines] -C lines -c Displays the sections of the two files that differ, including lines
(default is 3) around each line that diffs to show the context. Each line in file1
is missing from file2 is preceded by -, each extra line in file2 is preceded by + and
lines that have different versions in the two files are marked with ! When lines
are within three lines of each other, they are grouped together in the output.
--ed -e Creates a script for the ed editor, which will edit file1 to make it the same as file2,
ands sends it to standard output. You may add w (write) and q (quit) instructions to
t end of the script if you are redirecting input to ed the script. When you
use --ed, diff displays the changes in reverse order-changes to the end of the file are
listed before changes to the top. This prevents early changes from affecting later
changes when the script is used as input to ed. If made changes to the top of the file
first, the changes might affect later changes to the end of the file. For example, if a line
near the top were deleted, subsequent line numbers in the script would be wrong.