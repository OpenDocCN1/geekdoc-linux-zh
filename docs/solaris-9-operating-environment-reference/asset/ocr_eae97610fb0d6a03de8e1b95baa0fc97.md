# 248

# deroff

```
.B l
]
.B \-w
]
.B \-i
]
.IR filename |\.|\.||\|
]
```

SH DESCRIPTION
.IX "deroff command" " \fderoff\fP \em remove fLnroff\fP,
\fltroff\fP, \ltbl1\fP and \fL
e\fP constructs"
.IX "nroff utilities" "remove nroff/troff, tbl, and eqn constructs" "\remove fLnroff\fP,\n\fltroff\fP, \ltbl1\fP and \fLqn constructs \(em \fderoff\fP"
.IX "troff utilities" "remove nroff/troff, tbl, and eqn constructs" "\remove
fltroff\fP, \ltbl1\fP and \fLqn constructs \(em \fderoff\fP"
.IX "tbl" "remove nroff/troff, tbl, and eqn constructs" "\remove
\fLnroff\fP, \fltroff\fP,
\ltbl1\fP and \fLqn constructs \(em \fderoff\fP"
.IX "eqn" "remove nroff/troff, tbl, and eqn constructs" "\remove
\fLnroff\fP, \fltroff\fP,
\ltbl1\fP and \fLqn constructs \(em \fderoff\fP"
.IX "document production" "remove nroff/troff, tbl, and eqn constructs" ""
\remove fLnroff\fP, \fltroff\fP, \ltbl1\fP and \fLqn constructs \(em \fderoff\fP"

P,
B deroff
reads each
of the
.I filenames
in sequence
and removes all
.BR troff (1)
requests, macro calls constructs,
.BR eqn (1)
constructs
(between)
B \&.EQ
and
SM
...

castle@ deroff deroff.1

SMI;
Copyright AT&T

deroff Sep
NAME deroff remove nroff/troff, tbl, and eqn constructs
SYNOPSIS deroff
[