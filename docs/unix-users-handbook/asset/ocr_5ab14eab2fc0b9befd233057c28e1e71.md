Only LINK_MAX subdirectories can be created (see limits(5)).

# EXTERNAL INFLUENCES

# Environment Variables

LANG provides a default value for the internationalization variables that are unset or null. If LANG is unset or null, the default value of "C" (see lang(5)) is used. If any of the internationalization variables contains an invalid setting, mkdir will behave as if all internationalization variables are set to "C". See environ(5).

LC_ALL If set to a non-empty string value, overrides the values of all the other internationalization variables.

LC CTYPE determines the interpretation of text as single and/or multi-byte characters, the classification of characters as printable, and the characters matched by character class expressions in regular expressions.

LC MESSAGES determines the locale that should be used to affect the format and contents of diagnostic messages written to standard error and informative messages written to standard output.

NLSPATH determines the location of message catalogues for the processing of LC_MESSAGES.

# International Code Set Support

Single- and multi-byte character code sets are supported.

# DIAGNOSTICS

mkdir returns exit code 0 if all directories were successfully made. Otherwise, it prints a diagnostic and returns non-zero.

# EXAMPLES

Create directory gem beneath existing directory raw in the current directory:

```
mkdir raw/gem
```

Create directory path raw/gem/diamond underneath the current directory and set permissions on directory diamond to read-only for all users (a=r):

```
mkdir -p -m "a=r" raw/gem/diamond
```

which is equivalent to (see chmod(1)):

```
mkdir -p -m 444 raw/gem/diamond
```

If directories raw or raw and gem already exist, only the missing directories in the specified path are created.

# SEE ALSO

rm(1), sh(1), umask(1).

# STANDARDS CONFORMANCE

mkdir: SVID2, SVID3, XPG2, XPG3, XPG4, POSIX.2