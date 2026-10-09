```
$ grep sam *
memol:This is a letter to sam:
memol:not eating too much samak.
memo2:subsam ple by the end of the day.
memo5:sam, what is going on?

$ grep '^<sam' *
memol:This is a letter to sam:
memol:not eating too much samak.
memo5:sam, what is going on?

$ grep '^sam' *
memo5:sam, what is going on?
```

# OPTIONS

Count The -c (--count) option displays only the number of lines that contain a match in each file. The following example lists all files in the working directory, each followed by the number of times the regular expression (a simple string in this example) occurs in each file.

```
$ grep -c sam *
memol:2
memo2:1
memo3:0
memo4:0
memo5:1
```

Color The --color option causes grep to display the match in color on a terminal.

Extended regular expression The -E (--extended-regexp) option causes grep to accept extended regular expressions (page 1145). The following example uses an extended regular expression to display in color lines that contain a match for either vmx or svm in the /proc/cpuinfo virtual file, indicating whether the system supports hardware virtualization.

```
$ grep --color -E 'vmx|svm' /proc/cpuinfo
```

See page 664 for a slightly different version of this command. Calling grep with the -E option is the same as calling egrep.

Ignore case The -i (--ignore-case) option causes lowercase letters in the pattern to match uppercase letters in the file, and vice versa. This example lists all lines that contain the string sam with any combination of upper- and lowercase letters.

```
$ grep -i sam *
memol:This is a letter to sam:
memol:Dear Samuel --
memol:I hope this finds you and Sammy Jr. well and
memol:not eating too much samak.
memo3:subsam ple by the end of the day.
memo3:How is Sam doing?
memo5:sam, what is going on?
```