# # Appendix 14 Nested MIME attachments

This is based on an example in RFC-2046. If the content of Figure A14.1 is sent as a message, it's seen in Outlook Express as shown in Figure A14.2. Figure A14.3 shows how the delimiters structure the message into multiple and nested attachments.

# Figure A14.1
Contents of a message with nested MIME attachments

```
MIME-Version: 1.0
From: fred@example.com
To: jim@example.com
Date: Sat, 23 Mar 2002 12:15:17 +0000 (GMT)
Subject: A multipart example
Content-Type: multipart/mixed; boundary=unique-boundary-1

This is the preamble area of a multipart message.
Mail readers that understand multipart format
should ignore this preamble.

If you are reading this text, you might want to
consider changing to a mail reader that understands
how to properly display multipart messages.

--unique-boundary-1
This is the first attachment.
(Note that the blank between the boundary and the start of the text in
this part means no header fields were given and this is text in the
US-ASCII character set.)

--unique-boundary-1
Content-type: text/plain; charset=US-ASCII

This could have been part of the previous part, but illustrates
explicit versus implicit content-type specification for body parts.

--unique-boundary-1
Content-Type: multipart/parallel; boundary=another-separator

--another-separator
Content-Type: audio/basic
Content-Transfer-Encoding: base64

 [audio data goes here]
--another-separator
Content-Type: message/rfc822

From: jane@example.com
To: mary@example.com
Subject: hi!
Date: Fri, 22 Mar 2002 12:34:56 +0000 (GMT)
Content-Type: Text/plain; charset=ISO-8859-1
Content-Transfer-Encoding: Quoted-printable

Hello Mary
--another-separator
Content-Type: image/jpeg
Content-Transfer-Encoding: base64

 [image data goes here ...]
--another-separator--

--unique-boundary-1
Content-type: text/enriched

This is <bold><italic>enriched</italic></bold>
<smaller>as defined in RFC 1896</smaller>
Isn't it
<bigger><bigger>cool?</bigger></bigger>
--unique-boundary-1--
```