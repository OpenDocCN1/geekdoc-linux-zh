If GNU-compatible message files are processed, this option detects and diagnoses file anomalies that might represent translation errors.
The msgid and msgstr strings are studied and compared. It is considered abnormal if one string starts or ends with a newline and the other does not. Also, if the string represents a format string used in a printf-like function, both should have the same number of % specifiers, with matching types. If the flag c-format appears in the special comment # this entry, a check is performed.

# Examples

In the following example, module1.po and module2.po are portable message objects files.

```
castle cat module1.po
# default "messages.mo"
msgid "msg 1"
msgstr "msg 1 translation"
#
domain "help_domain"
msgid "help 2"
msgstr "help 2 translation"
#
domain "error_domain"
msgid "error 3"
msgstr "error 3 translation"
caste cat module2.po
# default "messages.mo"
msgid "mesg 4"
msgstr "mesg 4 translation"
#
domain "error_domain"
msgid "error 5"
msgstr "error 5 translation"
#
domain "window_domain"
msgid "window 6"
msgstr "window 6 translation"
caste%
```

The following command produces the output files,messages.mo, help_domain.mo, and error_domain.mo.
caste% msgfmt module1.po

The following command produces the output files,messages.mo, help_domain.mo, error_domain.mo, and window_domain.mo.
caste% msgfmt module2.po

The following example produces the output file -o hello.mo module1.po module2.po.
caste% msgfmt -o hello.mo module1.po module2.po