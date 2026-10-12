Normally, a digest list might have an open subscription policy. However, with a digest-only list, it should be closed.

```
# subscribe_policy [enum] (open) <majordomo> /open;closed;auto/
# One of 3 possible values: open, closed, auto. Open
# allows people to subscribe themselves to the list. Auto
# allows anybody to subscribe anybody to the list without
# maintainer approval. The existence of the file
# <listname>.auto is the same as specifying the value
# auto. Closed requires maintainer approval for all
# subscribe requests to the list. In addition to the
# keyword, if the file <listname>.closed exists, it is the
# same as specifying the value closed. The value of
# this keyword overrides the value supplied by any existent
# files.
subscribe_policy = closed
```

Whenever a digest is created, it is stored in ~majordomo/archives/digestonly-sample/ (that is, under the primary list name), and is mailed out to all the subscribers to the primary list.

# References

The 'Bat Book': Costales B and Allman E, Sendmail; O'Reilly. Check for the latest edition.

RFCs are available from many FTP archives. A Web or archive search on for example, RFC822, should provide many locations to fetch them from.

1523 Borenstein, N. The text/enriched MIME Content-type. 1993 September; 15 p. (Format: TXT=32692 bytes)

1522 Moore, K. MIME (Multipurpose Internet Mail Extensions) Part Two: Message Header Extensions for NonASCII Text. 1993 September; 10 p. (Format: TXT=22503 bytes) (Obsoletes 1342)

1521 Borenstein, N.; Freed, N. MIME (Multipurpose Internet Mail Extensions) Part One: Mechanisms for Specifying and Describing the Format of Internet Message Bodies. 1993 September; 81 p. (Format: TXT=187425 PS=393670 bytes) (Obsoletes RFC 1341)