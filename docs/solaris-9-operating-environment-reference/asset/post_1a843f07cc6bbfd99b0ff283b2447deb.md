
# zipinfo 1599

The following examples show how to display the full, short-format listing when the environment variable is set to turn off the totals line. Note that you must explicitly spec the -s option because the -t option by itself implies that only the totals line is to be printed.

```
castle$ setenv ZIPINFO --t
castle$ zipinfo -t 085XDOCS
4 files, 302592 bytes uncompressed, 105858 bytes compressed: 65.0%
castle$ zipinfo -st 085XDOCS
Archive: 085XDOCS.zip 106272 bytes 4 files
-rw-a-- 2.0 fat 76800 t-defn 18-Aug-98 21:55 085X1.DOC
-rw-a-- 2.0 fat 67072 b-defn 22-Aug-98 01:39 085X2.DOC
-rw-a-- 2.0 fat 95232 t-defn 31-Aug-98 20:29 085X42.DOC
-rw-a-- 2.0 fat 63488 t-defn 4-Oct-98 20:24 085X4E.DOC
4 files, 302592 bytes uncompressed, 105858 bytes compressed: 65.0%
castle$
```

The -s option lists -mand and -l, includes header and titles by default, unless spec otherwise. Because the environment variable specified no totals lines and that setting has a higher precedence than the default behavior of -s, you must use an explicit -t option to produce the full listing. Because nothing was indicated about the header, the -ts option is sufficient.

The following example lists information in detail about a single file within the archive.

```
castle$ zipinfo -m 085XDOCS1.DOC
-rw-a-- 2.0 fat 76800 -64% defN 18-Aug-98 21:55 085X1.DOC
castle$
```

When you specify any individual file with any of the format options, zipinfo displays only the single line of information about the requested file, regardless of the default specifications for header and titles. You can also add the -t option to the command.

The following example displays the first screen of information about the zip archive, using the verbose option and piping the output through the more(1) command.

```
castle$ zipinfo -v 085XDOCS | more
Archive: 085XDOCS.zip 106272 bytes 4 files
```

End-of-central-directory record:

```
Actual offset of end-of-central-dir record: 106250 (0001F0Ah)
Expected offset of end-of-central-dir record: 106250 (0001F0Ah)
(based on the length of the central directory and its (expected) offset)
```

This zipfile constitutes the sole disk of a single-part archive; its central directory contains 4 entries. The central directory is 226 (00000E2h) bytes long, and its (expected) offset in bytes from the beginning of the zipfile is 106024 (00019E28h).

There is no zip content.

Central directory entry #0:

# zipinfo

085X01.DOC

| Field | Value |
| :--- | :--- |
| offset of local header from start of archive: | 4 (00000004h) bytes |
| file system or operating system of origin: | MS-DOS, OS/2 or NT FAT |
| version of encoding software: | 2.0 |
| minimum file system compatibility required: | MS-DOS, OS/2 or NT FAT |
| minimum software version required to extract: | 2.0 |
| compression method: | deflated |
| compression sub-type (deflation): | normal |
| file security status: | not encrypted |
| extended local header: | no |
| file last modified on (DOS date/time): | 1998 Aug 18 21:55:14 |
| 32-bit CRC value (hex): | dcd305ce |
| compressed size: | 28048 bytes |
| uncompressed size: | 76800 bytes |
| length of filename: | 10 characters |

--

The following example shows the most recently modified files in the archive using the -T option in zipinfo with the sort(1) and tail(1) commands.

```
castle$ zipinfo -T 085XDOCS sort -n +6 | tail -15
Archive: 085XDOCS.ZIP 106272 bytes 4 files
--rw-a 2.0 76800 b-def 19990818.215514 085X01.DOC
--rw-a 2.0 67072 b-def 19990822.013496 085X02.DOC
--rw-a 2.0 95232 t-def 19990831.202906 085X02.DOC
--rw-a 2.0 63488 t-def 20240104.204202 085X04.DOC
--rw-a 2.0 50688 b-def 8-Jan-99 09:48 085X08.DOC
--rw-a 2.0 73238 t-def 1998-Dec-14 18:18 085X19.ELF
6 files, 44314 bytes uncompressed, 1439 bytes compressed: 67.4%
```

The -T option to sort(1) sorts numerically in ASCII order. The +6 option sorts the sixth field after the first one (that is, the seventh field). This counts as the default short-format list; if you use -or or -1, the proper sort(1) is +7. The tail(1) command filters out all but the last 15 lines of the listing. zipinfo may incorporate date/time and file-name as built-in options.

To display a list of files using the asterisk character, you must escape it by preceding it with a backslash. The following example shows information about three archives.

```
castle$ zipinfo *.ZIP
Archive: 085DOCS.ZIP 145031 bytes 6 files
--rw-a 2.0 76800 b-def 18-Jan-99 21:55:15 085X01.DOC
--rw-a 2.0 67072 b-def 22-Aug-98 03:19 085X02.DOC
--rw-a 2.0 80384 b-def 24-Sep-98 18:40 085X03.DOC
--rw-a 2.0 95232 t-def 19-Aug-98 20:29 085X04.DOC
--rw-a 2.0 50688 b-def 8-Jan-99 09:48 085X08.DOC
--rw-a 2.0 73238 t-def 1998-Dec-14 18:18 085X19.ELF
6 files, 150038 bytes uncompressed, 43099 bytes compressed: 71.3%
```

# zipinfo

2 archives were successfully processed.

# See Also
ls(1), unzip(1)

# URL
The Info-ZIP home page is currently at http://www.cdrom.com/pub/infozip

# Copyright
Distributed with permission from Info-ZIP. Please see http://www.cdrom.com/pub/infozip/doc/COPYING for copyright information.

# Author
Greg "Cave" Roofs. ZipInfo contains pattern-matching code by Mark Adler and improvements by many others. Please refer to source for a more complete list.

# Prentice Hall: Professional Technical Reference
Tomorrow’s Solutions for Today’s Professionals.

# Keep Up-to-Date with PTR Online!
We strive to stay on the edge of what's happening in professional computer science and engineering. Here's a bit of what you'll find when you stop at www.phptr.com:

- Special interest areas offering our latest books, book series, features of the month, related links and other useful information to help you get the job done.
- Deals, deals! Come to our promotions section for the latest bargains offered to you exclusively from our retailers.
- Need to find a bookstore? Chances are a bookseller near you that carries a broad selection of PTR titles. Locate a bookstore at www.phptr.com.
- What's new at PTR? We don't just publish books for the professional community, we're a part of it. Check out our convention schedule, join an author chat, get the latest reviews and press releases on topics of interest.
- Subscribe today! Join PTR's monthly email newsletter!
Want up-to-date on your area of interest? Choose a targeted category on our website, and we'll keep you informed of the PTR products, author events, reviews and conferences in your area.

Visit our mailbox to subscribe today! http://www.phptr.com/mail_lists

![](img/185d23104c385dfb6a62d4cc96b8997_1633_0.png)

# Inform IT Solutions from experts you know and trust.
Articles Free Library Expert Q & Training Career Center Downloads MyInformIT

Login Register About InformIT

# Topics
Operating Systems
Web Development
Programming
Security
Certification
Online

# www.informit.com
- Free, in-depth articles and supplements
- Master the skills you need, when you need them
- Choose from industry leading books, ebooks, and training products
- Get answers when you need them - from live experts or InformIT's comprehensive library
- Achieve industry certification and advance your career

# Expert Access

![](img/185d23104c385dfb6a62d4cc96b8997_1634_0.png)

Visit InformIT today and get great content from PH PTRFree Content
Prentice Hall and InformIT are trademarks of Pearson plc /
Copyright © 2000 Pearson

# GET READY!

Congratulations on taking control of your career! With Sun certification, you can enjoy the benefits of increased job opportunities, greater career advancement potential, and more professional respect.

The first step in preparing for exams is discovering what you need to know. The next step is discovering what you don't. To help you measure your skills and understand any gaps, Sun offers online skills assessments. They'll help you focus your energies on learning the skills that can lead certification. Online skills assessments are available at: http://suned.sun.com/USA/assessments.html.

# GET SET!

Preparation is the key to success, and this study guide is a good first step. However, our years of experience have taught us that few people learn in exactly the same way. So we've created innovative solutions that can augment this guide, including:

- Learning Solutions: Delivered via the Sun Learning Center, Sun's innovative eLearning solutions include Web-based training, online mentoring, ePractice exams, and the benefits of a community of like-minded people. Available by subscription, eLearning solutions give you anywhere, anytime learning—providing the flexibility you need to prepare according to your schedule, at your pace. You can visit the Sun Learning Center at http://suned.sun.com/WLC.
- Practice Exams: Also available through the Sun Learning Center, ePractice exams are practice tools that can help you prepare for Sun's certifications. The questions in the ePractice are written in the same format as the certification tests, helping you acquaint with the style of the actual certification exams. You get immediate results and recommendations for further study, helping you prepare and take your certification tests with more confidence. You can register for ePractice exams at http://suned.sun.com/US/wlc/.
- Instructor-Led Training: Sun's expert instructors provide unparalleled learning experiences designed to get you to speed quickly. Available at over 200 Sun locations worldwide or at your facility, instructor-led courses provide learning experiences that will last a lifetime.
- Self-Paced CD-ROM-based Training: Using JavaTutor, our CD-ROM-based learning solutions help you prepare for exams on your own terms, at your pace, in a dynamic environment. After you are certified, they'll serve as perfect reference tools.

# GO!

As you take your exams and become certified, go ahead and celebrate. For more information, visit: http://suned.sun.com.

Your road is wide open. Enjoy the journey.
