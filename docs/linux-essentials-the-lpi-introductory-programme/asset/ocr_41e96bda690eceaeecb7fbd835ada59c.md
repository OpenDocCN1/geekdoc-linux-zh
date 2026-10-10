Table 7.1: Regular expression support

| Extension | GNU grep | GNU egrep | trad egrep | vim | emacs | Perl | Tcl |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Word brackets | • | • | • | •1 | •1 | •4 | •4 |
| Grouping | •1 | • | • | •1 | •1 | • | • |
| Alternative | •1 | • | • | •2 | •1 | • | • |
| Option | •1 | • | • | •3 | • | • | • |
| At-least-once | •1 | • | • | •1 | • | • | • |
| Limits | •1 | • | ○ | •1 | •1 | • | • |
| Back-Reference | ○ | • | • | ○ | • | • | • |
| Non-Greedy | ○ | ○ | ○ | •4 | • | • | • |

• supported; ○: not supported

*Notes:* 1. Requires a preceding backslash ("\\"), e. g. "ab\\+" instead of "ab+". 2. Needs no parentheses; alternatives always refer to the complete expression. 3. Uses "*=" instead of "*?". 4. Completely different syntax (see documentation).

Table 7.2: Options for grep (selected)

| Option | Result |
| :--- | :--- |
| -c | (count) | Outputs just the number of matching lines |
| -i | (ignore) | Uppercase and lowercase letters are equivalent |
| -l | (list) | Outputs just the names of matching files, no actual matches |
| -n | (number) | Includes line numbers of matching lines in the output |
| -r | (recursively) | Searches files in subdirectories as well |
| -v | (invert) | Outputs only lines that do *not* match the regular expression |

💡 These observations used to be true to some extent. In particular, grep and egrep used completely different algorithms for regular expression evaluation, which could lead to wildly diverging performance results depending on the size and structure of the regular expressions as well as the size of the input. With the common Linux implementation of grep, all three variants are, in fact, the same program; they differ mostly in the allowable syntax for their search patterns.

+   syntax
+   grep's syntax requires at least a regular expression to search for. This is followed by the name of a text file (or files) to be searched. If no file name is specified, grep refers to standard input (see Chapter 8).
+   
+   regular expression
+   The regular expression to search in the input may contain, besides the basic regular expressions from Section 7.1, most of the extensions from Section 7.1.1. With grep, however, the operators "\\+", "\\?", and "\\(" must be preceded by a backslash. (For egrep, this is not necessary.) There are unfortunately no "non-greedy" operators.
+   
+   💡 You should put the regular expression in single quotes to prevent the shell from trying to expand it, especially if it is more complicated than a simple character string, and definitely if it resembles a shell search pattern.

+   In addition to the regular expression and file names, various options can be passed on the command line (see Table 7.2).
+   
+   Search pattern in file
+   With the -f ("file") option, the search pattern can be read from a file. If that file contains several lines, the content of every line will be considered a search pattern in its own right, to be searched simultaneously. This can simplify things considerably especially for frequently used search patterns.
+   
+   As mentioned above, fgrep does not allow regular expressions as search patterns. egrep, on the other hand, makes most extensions for regular expressions more conveniently available (Table 7.1).