Laboratories. But the port that Bell Labs had done did not support the VAX's virtual memory system. So, CSRg ported BSD to the VAX and added support for the VAX's virtual memory system.

CSRg made much of the BSD source code available to the public for free, and a man named Bill Jolitz ported BSD to the Intel x86 platform in 1991. The port was called 386/BSD. In addition, a commercial spin-off company of CSRg named Berkeley Software Distribution, Incorporated, sold a commercial version of BSD for the x86 platform that included source code.

# ## FreeBSD Is Born

In 1993, it became apparent that because of full-time jobs and such, Bill Jolitz was no longer going to enhance 386/BSD. Two different groups decided that the project was worth doing though. Therefore, two spin-off projects were formed. The first was NetBSD, which seemed to focus on universal availability. If it's a platform, chances are there is a version of NetBSD that runs on it. The second was FreeBSD, which focused on making the system easier to use for nontechnical users and also focused primarily on Intel x86 hardware (although, as mentioned previously, FreeBSD is now available for Alpha as well). Today, FreeBSD is the most popular of the BSD-based, Unix-like operating systems.

There are several more interesting events in the history of FreeBSD and Unix, such as the lawsuits over the Net/2 Tape, and more on the development of Unix. If you are interested in learning more about the history of FreeBSD and Unix, I recommend the following links:

+   - http://www.bell-labs.com/history/unix/ — Contains a detailed history of the development of Unix at Bell Labs, including some rare photographs.

+   - http://daemonz.org/bugs/history.html — Contains a detailed history of the Berkeley Software Distribution.

+   - http://www.freebsd.org/handbook/history.html — Contains more history of FreeBSD in particular.

# # The Design Philosophy of Unix

Several things have kept Unix going strong even after 30 years. One of these is its portability, as mentioned previously. In my opinion, however, the most important thing that has kept Unix on the cutting edge, when most other software that old is considered obsolete, is its design philosophy about how an operating system should work.

Many people tend to think of Unix as an extremely complicated, complex, and confusing operating system. But in my opinion, Unix is the ultimate example of the KISS (Keep It Simple, Stupid) design in an operating system. One of the amazing things about Unix is that it is both simple and extremely powerful at the same time. Here is how the designers of Unix did it.