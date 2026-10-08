original pathname have been removed.

When used in conjunction with the -i option, rmdir asks whether to remove each directory component of a path.

# EXTERNAL INFLUENCES

# Environment Variables

LANG provides a default value for the internationalization variables that are unset or null. If LANG is unset or null, the default value of "C" (see lang(5)) is used. If any of the internationalization variables contains an invalid setting, rmdir will behave as if all internationalization variables are set to "C". See environ(5).

LC_ALL If set to a non-empty string value, overrides the values of all the other internationalization variables.

LC_CTYPE determines the interpretation of dir names as single and/or multi-byte characters, the classification of characters as printable, and the characters matched by character class expressions in regular expressions.

LC_MESSAGES determines the locale that should be used to affect the format and contents of diagnostic messages written to standard error and informative messages written to standard output.

NLSPATH determines the location of message catalogues for the processing of LC_MESSAGES.

# International Code Set Support

Single- and multi-byte character code sets are supported.

# DIAGNOSTICS

Generally self-explanatory. Note that the -f option does not suppress all diagnostic messages.

# EXAMPLES

To remove directories with a prompt for verification:

```
rmdir -i directories
```

To remove as much as possible of a path, type:

```
rmdir -p component1/component2/dir
```

# SEE ALSO

rm(1), rmdir(2), stat(2).

# STANDARDS CONFORMANCE

rmdir: SVID2, XPG2, XPG3, XPG4