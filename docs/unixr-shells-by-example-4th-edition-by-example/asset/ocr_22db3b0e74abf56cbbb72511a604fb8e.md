# EXPLANATION (CONTINUED)

+   3 All filenames containing four characters are matched and listed if the filename starts with abc and is followed by a number in the range from 1 to 3.
+   4 All filenames containing three characters are matched and listed if the filename contains exactly three lowercase alphabetic characters.
+   5 All filenames containing four characters are listed if the first character is not a lowercase letter between f and z ([f-z]), followed by three of any character (e.g., ???).
+   6 Files are listed if the filenames contain abc12 followed by 2 or 3.

# 7.5.4 Escaping Metacharacters

To use a metacharacter as a literal character, the backslash may be used to prevent the metacharacter from being interpreted.

# EXAMPLE 7.17

+   1 $ ls
+   abc file1 youx
+   2 $ echo How are you?
+   How are youx
+   3 $ echo How are you\?
+   How are you?
+   4 $ echo when does this line \
+   > ever end?
+   when does this line ever end?

# EXPLANATION

+   1 The files in the present working directory are listed. (Note the file youx.)
+   2 The shell will perform filename expansion on the ?. Any files in the current directory starting with y-o-u and followed by exactly one character are matched and substituted in the string. The filename youx will be substituted in the string to read How are youx (probably not what you wanted to happen).
+   3 By preceding the question mark with a backslash, it is escaped, meaning that the shell will not try to interpret it as a wildcard.
+   4 The newline is escaped by preceding it with a backslash. The secondary prompt is displayed until the string is terminated with a newline. The question mark (?) is escaped to protect it from filename expansion.