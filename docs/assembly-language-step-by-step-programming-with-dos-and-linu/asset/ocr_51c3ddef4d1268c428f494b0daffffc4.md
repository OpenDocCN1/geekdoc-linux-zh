bly language geeks is in 1997, NASM, the Net-Wide Assembler, and it has improved relentlessly since its first release. Now, in 2000, it is brutally effective, easy to learn, and best of all, it's still free. I explain lots more about NASM through the course of this book, but you should fire up your Web browser and look at the NASM Web site at www.websites.co.uk/nasm/tools.html.

In the case of the book you own no longer has the CD-ROM in it, or if the CD-ROM is damaged or otherwise unreadable, you can download NASM from this Web site and many other places. The version of NASM I'm using throughout this book (the one that is on the CD-ROM) is 0.98. If you have an older version from somewhere, please obtain the 0.98 release so you don't get confused when I talk about features that don't exist in your copy!

Most commercial assemblers (such as MASM and TASM) come with their own special debugging tools, called debuggers. MASM's debugger is called Code, and TASM's debugger is called Turbo Debugger. Both are enormously sophisticated programs, and I won't be discussing either in this book, part due to their intimate connection with their associated assemblers, but mostly because there is a debugger shipped with every copy of DOS and Windows—even Windows NT. This debugger, simply named DEBUG, is more than enough debugger to cut your teeth on and will get you familiar enough debugger concepts to move up to a commercial debugger later on.

I describe DEBUG much more fully in a following section.

# Setting Up a Working Directory

The process of creating and perfecting assembly language programs involves a lot of different kinds of DOS files and numerous separate software tools. Unlike the tidy, fully integrated environments of Turbo Pascal, Delphi, or Visual Basic, assembly language development comes in a great many pieces with (as it were) some assembly required.

I recommend setting up a development subdirectory on your hard disk and putting all of the various pieces in that subdirectory. For ease of understanding, let's call this directory ASM. I've actually created an ASM directory for you on the CD-ROM that comes with this book. It is completely set up and ready to go, software and all, and all you need to