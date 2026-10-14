As we can see, tr operates on standard input and outputs its results on standard output. tr accepts two arguments: a set of characters to convert from and a corresponding set of characters to convert to. Character sets may be expressed in one of three ways.

+   - An enumerated list. For example, ABCDEFGHIJKLMNOPQRSTUVWXYZ.
+   - A character range. For example, A-Z. Note that this method is sometimes subject to the same issues as other commands because of the locale collation order and thus should be used with caution.
+   - POSIX character classes. For example, [:upper:].

In most cases, both character sets should be of equal length; however, it is possible for the first set to be larger than the second, particularly if we want to convert multiple characters to a single character.

```
[me@linuxbox ~]$ echo "lowercase letters" | tr [:lower:] A
AAAAAAAAA AAAAAAA
```

In addition to transliteration, tr allows characters to simply be deleted from the input stream. Earlier in this chapter, we discussed the problem of converting MS-DOS text files to Unix-style text. To perform this conversion, carriage return characters need to be removed from the end of each line. This can be performed with tr as follows:

```
tr -d '\r' < dos_file > unix_file
```

where dos_file is the file to be converted and unix_file is the result. This form of the command uses the escape sequence \r to represent the carriage return character. To see a complete list of the sequences and character classes tr supports, try the following:

```
[me@linuxbox ~]$ tr --help
```

tr can perform another trick, too. Using the -s option, tr can “squeeze” (delete) repeated instances of a character.