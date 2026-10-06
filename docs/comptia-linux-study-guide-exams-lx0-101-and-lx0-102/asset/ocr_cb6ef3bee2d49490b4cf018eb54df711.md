# Chapter 6 • Configuring the X Window System, Localization, and Printing

including punctuation and symbols. ASCII can't handle characters used in non-English languages, though it's awkward at best for international use. ISO-8859 was an early attempt to extend ASCII; it employs an eighth bit to extend ASCII by 128 characters, giving room for the characters needed by a small number of non-Roman alphabets. ISO-885 broken down into many standards, each of which handles one language or group of languages. ISO-8859-1 covers Western European languages and ISO-8859-5 provides Cyrillic support, for instance.

The latest codepage is the 8-bit Unicode Transformation Format (UTF-8). Like ISO, UTF-8 starts with ASCII but extends it by supporting variable-byte extensions so that a single character can take anywhere from one to four bytes to be encoded. This provides the ability to encode any text supported by Unicode, which is a character set designed to support as many languages as possible. The big advantage of UTF-8 over ISO-8859 is there's no need to specify a standard, such as ISO-8859-1 or ISO-8859-5; UTF-8 handles all of its variants automatically.

The *modifier* is a locale-specific code that modifies how it works. For instance, it may affect the sort order in a language-specific manner.

# What Is Your Locale?

A locale code can be assigned to one or more of several environment variables. To learn how these are set on your system, issue the locale command without any arguments:

```
$ /usr/bin/locale
LANG=en_US.UTF-8
LC_TYPE=en_US.UTF-8
LC_NUMERIC=en_US.UTF-8
LC_TIME=en_US.UTF-8
LC_COLLATE=en_US.UTF-8
LC_MONETARY=en_US.UTF-8
LC_MAGES=en_US.UTF-8
LC_PAPER=en_US.UTF-8
LC_NAME=en_US.UTF-8
LC_ADDRESS=en_US.UTF-8
LC_TELEPHONE=en_US.UTF-8
LC_MEASUREMENT=en_US.UTF-8
LC_IDENTIFICATION=en_US.UTF-8
LC_All=
```

As you can see, a few locale variables exist. When programs pay attention to these variables, they adjust appropriately for your locale. For instance, a word processor may default to using US paper sizes (such as 8.5 × 11 inches) when the territory code in LC_PAPER is set to US, European paper sizes (such as A4, 210 × 297 mm) when territory is set to a code for a country where those paper sizes are common.