So, while it is possible to write computer programs in pure binary (I have done it, but not since 1977), it's unpleasant work and will take you until the next Ice Age to accomplish anything useful.

The process of developing assembly language programs is a path that runs from whatever we call source code that you can read, to something called machine code that the CPU can execute. In the middle is a resting point called object code that we'll take a little later.

The process of creating true machine-code programs is one of translation. You must start with something that you and the rest of us can read and understand, and then somehow convert to something the CPU can understand and execute. Before examining either end of that road, however, we need to understand a little more about the land on which the road is built.

# The God Above, the Troll Below

Most of all, we need to understand DOS, both for its own sake and as sort of idiot brother of Linux. Some people look upon as a god; others as a kind of troll. In fact, DOS is a little of both. Mostly what you must put behind you is the common notion that DOS is a part of the machine itself and somehow resides in the same sort of silicon as the CPU. Not so DOS is a computer program of an only slightly special nature, called an operating system.

In part, an operating system is a collection of routines that do nothing but serve the hardware components of the computer itself. By hardware components I mean such things as disk drives, printers, scanners, and so on. DOS acts something like a troll living under the bridge to your disk drive. You tell the troll what you want to do with the disk drive, and the troll does it, his way, and at some cost (in machine cycles) to you.

You could write a program that handled every little aspect of disk operation itself (many game programmers have done exactly that) but it would be more trouble than it was worth, every program that runs on a computer needs to access the disk drives. And regardless of how grumpy the troll, he does get the job done, and assuming your disk drives aren't falling-down damaged does it right every time. Can you guarantee that you know all there is to know about running a disk drive? Forgive me if I have my doubts. That is, in my opinion, what trolls are for.