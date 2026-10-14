
and receive MIME mail on the command line, are useful for when you just use the mail tool to read and send occasional mail with an attachment, but the built-in methods for manipulating MIME mail in any reasonable MUA will invariably be easier and more convenient than the techniques described here (see section Picking the Right Mail Application).

- 31.4.1 Reading a Mail Attachment
- Reading mail attachments.
- 31.4.2 Sending a Mail Attachment
- Sending mail attachments.

## 31.4.1 Reading a Mail Attachment

To read a mail attachment, write the message to a file and then run metamail with the file name as an argument. metamail lists each attachment and prompts you about whether it should display the attachment, write it to a file, or skip it.

To read a mail attachment, type:

```
$ mail RET
Mail version 8.1 6/6/93. Type ? for help.
"/var/spool/mail/m": 1 messages 1 new
62;N 1 Photo Dept. Mon Feb 12 14:37 231/10980 "New Images"
38; w1 image.mail RET
"image.mail" [New file]
38; x RET
$ metamail image.mail RET
```

In this example, the mail tool was used to open the INBOX and write the message to a file called `image.mail`; then, metamail was run with the file name as an argument.

## 31.4.2 Sending a Mail Attachment

To send a file as an email attachment, use metasend. It prompts for the values to use in the `To:`, `Subject:`, and `CC:` header fields, plus the following values for each MIME attachment: its `Content-type:` field, which describes the kind of data the attachment contains; the file name; and the type of encoding to use, if any (usually one is recommended).

- To mail the JPEG file `dream.jpeg` in the current directory to the address dali@example.org, type:

```
$ metasend RET
To: dali@example.org RET
Subject: The image you requested RET
CC: RET
Content-type: image/jpeg RET
Name of file containing image/gif data: dream.jpeg RET
Do you want to encode this data for sending through the mail?
1 -- No, it is already in 7 bit ASCII
2 -- Yes, encode in base64 (most efficient)
3 -- Yes, encode in quoted-printable (less efficient, more readable)
4 -- Yes, encode it using uuencode (not standard, being phased out)
2 RET
Do you want to include another file too (y/n) [n] ? n RET
Delivering mail, please wait... Mail delivery apparently succeeded.
$
```

The following table lists values to use in the MIME `Content-type:` field for various kinds of files.

| VALUE | FILE TYPE |
| --- | --- |
| application/gzip | File compressed with gzip. |
| application/zip | File compressed with zip. |
| application/postscript | PostScript file. |
| image/jpeg | JPEG image file. |
| image/png | PNG image file. |
| audio/basic | Audio file. |
| audio/mpeg3 | MP3 audio file. |
| audio/wav | WAV audio file. |

## 31.5 Making an Email Signature

```
@sf(Debian): `sigrot`
@sf(WWW): `ftp://metalab.unc.edu/pub/linux/system/mail/misc/`
```

A signature file (often called a "dot sig," and written as `.sig`) is a text file containing text that you want to appear at the end of email messages and other online postings.

Sometimes, people put their name, email address, and a small quote, or a piece of ASCII art (such as text written in a figlet font---see section Horizontal Text Fonts); once the World Wide Web became popular, many people started including the URL of their home page in their `.sig`.

The use of signatures goes in and out of vogue with the years; you can decide whether or not you want to use one, but whatever you do, be sure to keep your `.sig` at most four lines in length---to use any more is considered very bad form. A first line consisting only of `-- ` is sometimes used; many applications recognize this text as the beginning of a `.sig` when processing messages.

You create your signature file in a text editor, just like any other text file. Name the file `.signature` or `.sig`, and keep it in your home directory.

If you want to use more than one signature, use sigrot to "rotate" your various signatures—every time you run sigrot, it selects one of the signature files you keep in your `.sigrot` directory and writes it to `.signature`. To change your `.signature` every time you log in, you would run sigrot in your `.bash_login` file (see section The Shell).

## 31.6 Picking the Right Mail Application

The following table lists some of the more popular MUAs that are available for Linux, describing their special features, and listing their Debian package name and URL (when available).

APPLICATION DESCRIPTION

balsa
A graphical email client that works in X with GNOME installed; its interface is inspired somewhat by the proprietary Eudora. {@sf{Debian}}: `balsa` {@sf{WWW}}: http://www.balsa.net/

elm
A menu-driven MUA, elm was popular in the early 1990s among experienced users—it has some interesting features, including ways to send mails in batch mode to many addresses at once, and a tool to send telephone messages as email messages. Interest in elm has waned somewhat over the years, and most novices are advised to try mutt instead. {@sf{Debian}}: `elm me+` {@sf{WWW}}: http://www.instinct.org/elm/

gnus
The gnus newsreader for Emacs(39) can also be used to read and send mail. It has many features and should appeal to Emacs lovers—but a warning: it can be daunting to learn! {@sf{Debian}}: `gnus` {@sf{WWW}}: http://www.gnus.org/

mew
mew is an Emacs mail and news facility developed in Japan. It shows promise as a fairly new MUA and has many features for handling mail in complex ways. {@sf{Debian}}: `mew` {@sf{WWW}}: http://www.mew.org/
