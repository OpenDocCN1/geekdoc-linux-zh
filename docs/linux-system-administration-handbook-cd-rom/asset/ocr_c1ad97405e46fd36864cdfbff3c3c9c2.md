current preference is mutt, because it has the ease of use of elm, plus a lot
more configurability and integrated Pretty Good Privacy (PGP) support.

# 7.3 MIME

When SMTP was first designed, it would handle only 7-bit (plain ASCII)
data. Hence, the “Simple” in the protocol name. With things like JPEG
images, sound files, application data, and compressed data, there had to be
some way of sending this binary (8-bit) data through a 7-bit stream. The first
method of handling this was via the uuencode program. This program would
turn 2 bytes of 8-bit data into 3 bytes of 7-bit data. The file size was larger,
but it would now squeeze through the 7-bit path that SMTP provided.
Another problem besides the file size was that the remote side had to decode
data (undecode). This turned into a tedious procedure, the sender encoder-
ing the data and manually including it in a mail file and the receiver trying to
strip out all the mail headers, text, and signatures to get to the uuucode file
 then decode it.

In the early 1990s, the Multipurpose Internet Mail Extension (MIME)
was developed to do this, and it is used today on the Web for determining file
types. MIME encoded the data such that a standard way of locating and
decoding a file would be used. Once a filetype was detected, each individual
user could have a file (.mailcap) that would list what filetypes you knew
about, and what application to run once you found a certain filetype.
example, if a JPEG image was sent, the receiving side might start the xv
program. Another user might have it set so the image is converted into
PostScript and sent directly to the printer.³ Most mailers today have the abil-
ity to handle MIME mail, and there should be little to no interaction that you
as an administrator have to worry about, except for installing programs for
users and occasionally editing the /etc/mailcap file (the default mailcap file
for all users) to add any new entries you come across.

# 7.4 The .forward File

When mail comes in, the .forward file is checked. If it exists, the E-mail is
ent to the address listed in the file. This is helpful if you have multiple

> ³This is a good example of “the UNIX way”—there’s more than one way to do
anything.