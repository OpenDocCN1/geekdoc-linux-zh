
- Policies and procedures ................................................................................................ 1215
- The difference between policies and procedures ............................................................ 1215
- Policy best practices ....................................................................................................... 1216
- Procedures ........................................................................................................................ 1216
- Disaster recovery .......................................................................................................... 1217
- Risk assessment ......................................................................................................... 1217
- Disaster management ....................................................................................................... 1218
- Staff for a disaster ...................................................................................................... 1220
- Power and HVAC ............................................................................................................ 1220
- Internet connection redundancy ...................................................................... 1221
- Security incidents ....................................................................................... 1222
- Compliance: regulations and standards ................................................................ 1222
- ITIL: the Information Technology Infrastructure Library ................................... 1225
- NIST: the National Institute for Standards and Technology ................................ 1225
- Legal issues ......................................................................................................... 1226
- Privacy ....................................................................................................................... 1226
- Policy enforcement ....................................................................... 1227
- Control = liability ....................................................................................... 1228
- Software licenses .................................................................................. 1228
- Organizations, conferences, and other resources ....................................... 1229
- Recommended Reading ...................................................................................... 1231
- Exercises ................................................................................................................ 1231

# INDEX .......................................................................................................... 1233

# A BRIEF HISTORY OF SYSTEM ADMINISTRATION ................................ 1264

# IN DEFENSE OF AIX ............................................................................ 1274

# COLOPHON ................................................................................................ 1277

# ABOUT THE CONTRIBUTORS ....................................................... 1278

# ABOUT THE AUTHORS .......................................................................... 1279

# Foreword

Twenty-seven years ago, in 1983, I wrote what may have been the first system administrator’s guide for the UNIX operating system. I'd been hired as a contractor to write documentation at a UNIX workstation company called Massachusetts Computer Company (MASSCOMP for short). When I finished the graphics programming manuals I'd been hired to write, I was casting around something else to do. "When any of us system problems, we go to Tom Teixeira," I said. "What are our customers going to do?"

The answer was quick: "Uh, oh! We really need a manual." I was soon rehired to extract as much information as I could from Tom Teixeira’s and put it onto paper.

That book covered the basics: the root account, account addition, permission management, backup and restore, a bit about networking with UUCP, and so on. It was oriented toward System V, one of the two dominant flavors of UNIX at the time (the other being Berkeley UNIX).

All things considered, I did a pretty good job of extracting information from Tom and other members of the then caste of elite system administrators. But there was no question in my mind that the UNIX System Administration Handbook (USAH) came out in 1989, the bible of the field had arrived—captured by an amanuensis, but direct from the keyboards of the masters.

By then, O'Reilly had become a publisher. Recognizing that many of my technical writing customers were adopting UNIX, I had begun regaining the rights to the manuals I wrote so that I could resell them to other companies. In late 1985, we introduced our first books that were sold to the public rather than licensed to companies. We focused first on small books about individual topics as vi, sed and awk, termcap and terminfo, and the UUCP networking system. We called them “Nutshell Handbooks” because we wanted to capture everything “in a nutshell”.

We didn't really know anything about publishing. Our books had no spines (they were stapled), indexes, or ISBNs. We sold them by mail order, not through bookstores. But by bit by bit, we learned. And eventually, we came into competition with the existing world of computer book publishers.

Eventually, as our business matured and we entered the retail computer book market, we realized that competition could help grow the market. People see one book, and it's an outlier. They see more than one, and, to quote Arlo Guthrie, “they may think it’s a movement.” Beside, in that first edition of USAH, the authors had a clear bias toward BSD-based systems, and we thought there was room for a book with more of a System V bias.

In 1991, we published our own comprehensive book on UNIX system administration, Ellen Frisch’s Essential System Administration.

As an author, editor, and publisher, I never paid attention to the competition—except in a few cases. This is one of those cases. The UNIX System Administration Handbook is one of the few books we measured ourselves against. Could we be as good? Could we be better? Like the NBA duels of Magic Johnson and Larry Bird, the competition brought out the best in us.

Uh, oh again! Fourth edition? Æleen had better get back to work! :)

Tim O'Reilly
June 2010

# Preface

When we were writing the first edition of this book in the mid-1980s, we were eager to compare our manuscript with other books about system administration. To our delight, we could find only three. These days, you have your choice of hundreds. Here are the features that distinguish our book:

- We take a hands-on approach. You already have plenty of manuals; or our purpose is to summarize our collective perspective on system administration and to recommend approaches that stand the test of time. This book contains numerous war stories and a wealth of pragmatic advice.
- This is not a book about how to run UNIX or Linux at home, in your garage, or on your PDA. We describe the management of production environments such as businesses, government offices, and universities.
- We cover networking in detail. It is the most difficult aspect of system administration and the area in which we think we can be of most help.
- We cover the major variants of UNIX and Linux.

# THE ORGANIZATION OF THIS BOOK

This book is divided into three large chunks: Basic Administration, Networking, and Bunch o' Stuff.

Basic Administration presents a broad overview of UNIX and Linux from a system administrator's perspective. The chapters in this section cover most of the facts and techniques needed to run a stand-alone system.

The Networking section describes the protocols used on UNIX systems and the techniques used to set up, extend, and maintain networks and Internet-facing