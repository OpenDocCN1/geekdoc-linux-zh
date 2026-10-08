DIAGNOSTICS
line too long Line length must not exceed LINE_MAX characters or fields, including the new-line character (see limits(5).

bad list for b/c/f option Missing -b, -c, or -f option or incorrectly specified list. No error occurs if a line has fewer fields than the list calls for.

no fields list is empty.

WARNINGS
cut does not expand tabs. Pipe text through expand(1) if tab expansion is required.

Backspace characters are treated the same as any other character. To eliminate backspace characters before processing by cut, use the fold or col command (see fold(1) and col(1)).

AUTHOR
cut was developed by OSF and HP.

SEE ALSO
grep(1), paste(1).

STANDARDS CONFORMANCE
cut: SVID2, SVID3, XPG2, XPG3, XPG4, POSIX.2