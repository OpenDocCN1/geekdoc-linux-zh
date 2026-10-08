Environment Variables
LC_CTYPE determines the locale for the interpretation of text as single- and/or multi-byte characters.
LC_MESSAGES determines the language in which messages are displayed.
If LC_CTYPE or LC_MESSAGES is not specified in the environment or is set to the empty string, the value of LANG is used as a default for each unspecified or empty variable. If LANG is not specified or is set to the empty string, a default of "C" (see lang(5)) is used instead of LANG.
If any internationalization variable contains an invalid setting, split behaves as if all internationalization variables are set to "C". See environ(5).

International Code Set Support
Single- and multi-byte character code sets are supported.

SEE ALSO
bfs(1), csplit(1).

STANDARDS CONFORMANCE
split: SVID2, SVID3, XPG2, XPG3, XPG4, POSIX.2