+   - RFC-2046 November 1996 (MIME) Part Two: Media Types

+   - RFC-2047 November 1996 (MIME) Part Three: Message Header Extensions for Non-ASCII Text

+   - RFC-2048 November 1996 (MIME) Part Four: Registration Procedures

+   - RFC-2049 November 1996 (MIME) Part Five: Conformance Criteria and Examples

+   - RFC-2183 August 1997 Communicating Presentation Information in Internet Messages: The Content-Disposition Header Field

The Internet Assigned Numbers Authority (IANA) acts as a central registry for defined MIME keywords. For a list of types and subtypes, see:

+   - [http://www.iana.org/assignments/media-types](http://www.iana.org/assignments/media-types)

The fact that it was possible to introduce MIME without breaking all non-MIME systems at the time is a good example of the old principle "Be conservative in what you send and liberal in what you receive." Just by ignoring the MIME-able headers, all non-MIME mailers were able to receive MIME messages; they weren't able to display or extract the contents, but often the user could do this manually, if it was important enough. If instead the mail systems were "conservative in what they received," they would have rejected MIME messages on the grounds that they couldn't understand the headers. That would have been a Bad Thing.

# IMAP

The early RFCs contain good discussions of the motivation for IMAP and are better introductions than later standards:

+   - RFC-1176 August 1990 Interactive Mail Access Protocol: Version 2

The original and current standards for IMAP, Version 4 are respectively:

+   - RFC-1730 December 1994 Internet Message Access Protocol – Version 4

+   - RFC-2060 December 1996 Internet Message Access Protocol – Version 4rev1

The Internet Mail Consortium, at:

+   - [http://www.imc.org](http://www.imc.org)

has a list of mail-related RFCs, and more importantly a list of mail-related Internet drafts – which are indicators of possible future developments in Internet e-mail. At the time of writing, several of these drafts relate to IMAP.

# Microsoft Exchange

For details of the ports Exchange uses for "Outlook Web Access," i.e. its Web-mail add-on, and for an indication of the complexity of Exchange, see:

+   - MS-KB-Q176466 XGEN: TCP Ports and Microsoft Exchange: In-depth Discussion

+   - [http://www.microsoft.com/exchange/techinfo/outlook/2000/0WA2000.asp](http://www.microsoft.com/exchange/techinfo/outlook/2000/0WA2000.asp)