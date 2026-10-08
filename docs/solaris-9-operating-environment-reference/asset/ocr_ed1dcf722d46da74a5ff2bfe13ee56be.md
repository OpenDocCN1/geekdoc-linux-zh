# 1474

# uniq

+   -s chars Ignore first chars characters when doing comparisons, where chars is a positive decimal integer. If specified in conjunction with the f option, ignore the first chars characters after the first fields. If chars specifies more characters than remain on an input line, use a null string for comparison.

+   -u Suppress the writing of lines that are repeated in the input.

+   -n Equivalent to -f fields with fields set to n.

+   +m Equivalent to -s chars with chars set to m.

# Operands

input-file A path name of the input file. If you do not specify input-file or if the input-file is -, use the standard input.

output-file A path name of the output file. If you do not specify output-file, use the standard output. The results are unspecified if the file named by output-file is the file named by input-file.

# Examples

The following example lists the contents of the uniq.test file and outputs a copy of the repeated lines.

```
castle@ uniq.test
This is a test.
This is a test.
TEST.
Computer.
TEST.
TEST.
Software.
caste@ uniq -d uniq.test
This is a test.
castle@
```

The following example outputs just those lines that are not repeated in the uniq.test file.

```
castle@ uniq -u uniq.test
TEST.
Computer.
Software.
caste@
```

The following example precedes each line with a count of the number of times each line occurred in the file.

```
castle@ uniq -c uniq.test
2 This is a test.
1 TEST.
1 Computer.
```