
## Contents

**Part V**
**Advanced Linux Networking**

- **23 Backups** ... 441
    - Evaluating Your Backup Needs ... 442
    - Managing the Backup Device and Files ... 443
    - Using mkfs to Create the Device Files ... 445
    - Manipulating the Tape Device with mt ... 445
    - Command-Line Tools ... 446
    - dump and restore ... 446
    - tar ... 450
    - Summary ... 451

- **24 Network Configuration** ... 455
    - Networking 101 ... 456
        - IP Addresses ... 456
        - CIDR ... 459
    - Modules and Network Interfaces ... 459
    - ifconfig ... 460
        - Simple Usage ... 460
        - Additional Parameters ... 462
    - Using route ... 463
        - Simple Usage ... 464
    - Displaying Routes ... 465
    - Summary ... 467

- **25 Advanced Linux Networking** ... 489
    - IP Aliasing ... 470
    - Packet Filtering ... 471
        - How Packet Filtering Works ... 472
        - ipchains ... 476
        - Cookbook Solutions ... 483
    - IP Masquerading ... 487
        - The Three-Line IP Masquerading Solution ... 489
        - Masquerading Proxies ... 490
    - Summary ... 491

- **26 The /proc File System** ... 493
    - What's Inside the /proc File? ... 494
    - Tweaking Files Inside of /proc ... 495
    - Some Useful /proc Entries ... 495
    - Enumerated /proc Entries ... 498
    - Common Reports and Settings Done with /proc ... 498
    - SYN Flood Protection ... 498
    - Issues on High-Volume Servers ... 499
    - Debugging Hardware Conflicts ... 499
    - Summary ... 500

**Appendices**

- **A** Programming Languages that Accompany Red Hat Linux ... 501
- **B** Getting the Usual Done ... 507
- **Index** ... 513

## ACKNOWLEDGMENTS

My personal tip to all would-be authors out there: Don’t start a book project right after you get married. Despite my making this incredibly stupid mistake, Heidi, my wonderful wife and best friend, has decided to keep me and I will be forever grateful. This book was in direct competition with her for my attention and free time, yet she supported its creation from start to finish and demonstrated amazing patience every time I came home on a Friday night and told her that I had to keep working. Even more amazing was that she’d get on my case when my “10-minute break” would start lasting too long and soon got me going again. This book is as much her sacrifice as it is mine. Heiði: If I ever decide to act older than a 13-year-old, I want you to be my teacher.

Before Heiði came to my rescue, my wonderful family made it possible for me to learn volumes about the world of technology around me. And for that, I thank my parents, Manjari and Jagdish, as well as my sister Mona.

I never understood why authors would always thank their editors so much. I mean, doesn't the author do the hard work? Then I actually wrote a book and understood. I was blessed with editors who were not only great at their jobs but showed incredible patience with me as well. Jane Brownlow and Tara Davis should get medals for their work. My tech editor and good friend, Art Chan (who also helped bail me out of a slipping schedule by authoring the DHCP chapter) didn't let me get away with omitting the details that ended up making this book something that I'm very proud of. What Art did technically, Carol Henry did grammatically. This book is understandable because Carol replaced what I wrote with English, and for that I'm extremely grateful. And last but certainly not least, cheers to Madhu Prasher and her squadron of artists, who took the text along with my hand-drawn "artwork" and turned it all into a book. My hat's off to all of them.

Along with my wife, family, and editors, I am grateful to my coworkers at Ateeon Web Systems, who have been kind enough to put up with my whining for so long. They make work a fun place to be, and as a result I was left with enough energy to keep working when I got home. And cheers to the gang at Syzygy, who introduced me to UNIX in the first place.

I also want to thank all the developers who make Linux a system I love talking about, writing about, and working with day to day. They make it possible for me to stand in front of managers and clients and tell them that Linux is a real solution to their problems.

Finally, thanks to all the great teachers I've had. It's their dedication that made it possible for me to succeed.

## INTRODUCTION

System administrators are a unique bunch. As a group, we are probably the most significant consumers of reference and training books, and we probably demand the most from them (at least, all of my peers do). And, of course, we get really annoyed with books that waste our time. We're also a curious bunch. Most of my IT friends are gadget freaks (my wife included). We love to live on the edge of new technologies and find out what the buzz is about before our users do. We like to learn about new stuff for two very simple reasons: because it's fun, and because we need to understand the technology before the CEO hears about it in *Business Week* and demands to know why we aren't running it. And Linux, it seems, is one of the buzzes.

## Linux Administration: A Beginner's Guide

Deidrakh will argue that Linux has been a buzz since the mid-1990s (it’s been available since 1991). I personally started introduced Linux in 1994 when some friends of mine suggested I make better use of my "huger" 340MB hard disk. I deployed Linux as a server operating system in 1995, when a coffee shop in my area decided to become a "cyber-café." In 1997, Linux became mature enough for me to deploy it as a primary server in a 100-user office environment, where server crashes meant being paged at any hour of the night. Linux held up well in those roles, but even I will agree that it didn't hit the limelight until the big players of the industry decided it was noteworthy. (One of my favorite comic strips shows a Penguin, the Linux mascot, strapped to a large jet engine labeled “IBM.” with the caption “How do you make a Penguin fly?”)

But when IBM started porting DB2 to Linux, SGI adopted Linux as one primary desktop OS, and even Dell made Red Hat Linux a preinstallation option on servers—that’s what started the real buzz.

### WHO SHOULD READ THIS BOOK

The title of this book says it’s a “beginner’s guide,” and that’s mostly true. What the title should really say is that it’s a “beginner-to-Linux guide,” because we do make a few assumptions about you, the reader.

First, we assume you are already familiar with the Windows environment. To the very least, you should be a strong user in Windows and know something about the networked Windows environment. Although you needn’t be an NT expert, some exposure to NT will help your understanding of the hoisted concepts we discuss. We started with this assumption because we didn’t want to waste time repeating what most folks from a Windows background already know, focusing instead on the new stuff that Linux brings to the table.

In addition to your Windows background, we assume that you’re interested in having more information about the topics introduced here. After all, we’re spending 30 or 40 pages on topics with entire books devoted to them! So every chapter here includes references to other texts. We urge you to take advantage of these references-no matter how advanced you think you’re becoming, there is always more to learn.

### WHAT’S IN THIS BOOK

*Linux Administration: A Beginner’s Guide* is organized into five parts.

- **PART 1** The first part is targeted at folks with no experience in Linux and who want a hand installing it and getting rolling.
    - Chapter 1 focuses on the architectural differences between NT and Linux and will help you understand why some things in the Linux environment are the way they are.
    - Chapter 2 puts a unique spin on an installation chapter: Instead of just regurgitating installation notes from the product, we help you specifically configure your Linux system
