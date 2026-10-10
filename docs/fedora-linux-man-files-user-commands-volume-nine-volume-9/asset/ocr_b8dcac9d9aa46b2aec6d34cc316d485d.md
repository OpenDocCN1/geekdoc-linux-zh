# **-u, --utf8**

By default, **pod2man** produces the most conservative possible *roff output to try to ensure that it will work with as many different *roff implementations as possible. Many *roff implementations cannot handle non-ASCII characters, so this ans all non-ASCII characters are converted either to a *roff escape sequence that tries to create a properly accented character (at least for troff output) or to X.

This option says to instead output literal UTF-8 characters. If your *roff implementation can handle it, this is the best output format to use and avoids corruption of docunts containing non-ASCII characters. However, be warned that *roff source with literal UTF-8 characters is not supported by many implementations and may even result in segfaults and other bad behavior.

Be aware that, when using this option, the input encoding of your POD source st be properly declared unless it is US-ASCII or Latin-1. POD input without an `=encoding` command will be assud to be in Latin-1, and if it’s actually in UTF-8, the output will be double-encoded. See (1) for more information on the `=encoding` command.

# **-v, --verbose**

Print out the na of each output file as it is being generated.