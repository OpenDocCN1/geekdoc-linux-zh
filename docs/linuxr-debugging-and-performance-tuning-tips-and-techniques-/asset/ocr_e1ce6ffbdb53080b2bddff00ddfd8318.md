Besides the original `msgid` argument, these functions accept additional arguments:

```
const char *msgid_plural
```

The default string to use for plural values. Examples shortly.

```
unsigned long int n
```

The number of items there are.

Each locale's message catalog specifies how to translate plurals.⁸ The `ngettext()` function (and its variants) examines `n` and, based on the specification in the message catalog, returns the appropriate translation of `msgid`. If the catalog does not have a translation for `msgid`, or in the `"C"` locale, `ngettext()` returns `msgid` if `n == 1`; otherwise, it returns `msgid_plural`. Thus, our misspelled words example looks like this:

```
printf("%s\n", ngettext("%d word misspelled", "%d words misspelled", nwords), nwords);
```

Note that `nwords` must be passed to `ngettext()` to select a format string, and then to `printf()` for formatting. In addition, be careful not to use a macro or expression whose value changes each time, like `n++`! Such a thing could happen if you're doing global editing to add calls to `ngettext()` and don't pay attention.

# ### 13.3.4 Making gettext() Easy to Use

The call to `gettext()` in program source code serves two purposes. First, it does the translation at runtime, which is the main point, after all. However, it also serves to *mark* the strings that need translating. The `xgettext` utility reads program source code and extracts all the original strings that need translation. (We briefly cover the mechanics of this later in the chapter.)

Consider the case, though, of *static strings* that aren't used directly:

```
static char *copyrights[] = {
"Copyright 2004, Jane Programmer",
"Permission is granted ...",
... ,
NULL
};
```

*LOTS of legalese here*