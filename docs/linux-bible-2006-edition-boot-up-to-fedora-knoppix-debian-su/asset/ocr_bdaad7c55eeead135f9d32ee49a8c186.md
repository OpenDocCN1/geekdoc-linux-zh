# Part I ♦ Linux Firsts

Linus (torvalds@kruuna.helsinki.fi)
it is free of any minix code, and it has a multi-threaded fs. It is NOT portable[sic] (uses 386 task switching etc), and it probably will never support anything other than AT-hardds, as that's all I have :-(

> Reprinted from Linux International Web site
(www.li.org/linuxhistory.php)

Minix is a UNIX-like operating system that ran on PCs in the early 1990s. Like Minix, Minix was also a clone of the UNIX operating system. To truly appreciate how free operating system could have been modeled after a proprietary system from AT&T Bell Laboratories, it helps to understand the culture in which UNIX created and the chain of events that made the essence of UNIX possible to reproduce freely.

# From a Free-Flowing UNIX Culture at Bell Labs

From the very beginning, the UNIX operating system was created and nurtured in a communal environment. Its creation was not driven by market needs, but by a desire to overcome impediments to producing programs. AT&T, which owned the UNIX trademark, eventually made UNIX into a commercial product, but by that time, many of the concepts (and even much of the early code) which made UNIX special had fallen into the public domain.

If you are 30 years old, you might not remember a time when AT&T was "the" phone company. Until the early 1980s, AT&T didn't have to think much about competition if you wanted a phone in the United States, you would have to go to AT&T. It had the luxury of funding research projects. The Mecca for such projects was the Bell Laboratories in Murray Hill, New Jersey.

After the failure of a project called Multics in 1969, Bell Labs employees Ken Thompson and Dennis Ritchie set out to create an operating system that would offer an improved environment for developing software. Up to that time, programs were written on punch cards that had to be fed in batches of frame computers. In a 1980 lecture "The Evolution of the UNIX Time-sharing System," Dennis Ritchie summed the spirit that started UNIX:

What we wanted to preserve was not just an environment in which to do programming, but a system around which a fellowship could form. We knew from experience that the essence of communal computing as supplied by remote-access, time-shared machines is not just to type programs into a ter terminal instead of a keypunch, but to encourage close communication.

The simplicity and power of the UNIX design began breaking down barriers that impeded software developers. The foundation of UNIX was set with several key elements: