# Options

Put the output in filename. The format of entries in filename is a name (C variable), followed by one or more regular expressions, enclosed in double quotes. The output of regcmp is C source code. Compiled regular expressions are represented as extern filename.i files can be #included in C programs, and filename.c files can be compiled and loaded. In the C program that uses the regcmp output, regex (abc, line) applies the regular expression named abc to line. Diagnostics are self-explanatory.

# Examples

In the following example, the three arguments to telno must be entered on one line.

```
telno  "([A-Za-z] [A-Za-z0-9_]*)\$"
       \((0|1)) [[2-9]] [[1-9]] $0)\{0,1} **
       "({{0-9] [0-9]){2} $1[-])\{0,1}"
       "({{0-9]{4}) \$2"
```

In the C program that uses the regcmp output, the following statement applies the regular expression named telno to line.

```
regex(telno, line, area, exch, rest)
```

# Environment Variables

See environ(5) for a general description of the LC_* environment variables.

Determine how regcmp handles characters. When LC_TYPE is set to a valid value, regcmp can display and handle text and file names containing valid characters for locale.

LC_TYPE

Determine how diagnostic and informative messages are presented, including the language and style of the messages and the correct form of affirmative and negative responses. In the C locale, the messages are presented in the default format found in the program itself(in most cases, U.S. English).

LC_MESSAGES

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | Suntoo |
| CSI | Enabled |

# See Also

regcmp(3C), attributes(5), environ(5)