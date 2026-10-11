
In the chapters that follow, system administrators will learn how to adapt a kernel to specific needs and hardware environments. In addition, by tuning the kernel in the appropriate places, system throughput can be increased considerably. The File Systems section of this book discusses choosing, installing, and correctly configuring a file system. Linux developers will learn which programming techniques yield the best performance for their programs and debugging will be easier after reading this book because external factors to the user programs will be better understood.

Finally, Linux enthusiasts in general, will learn to appreciate their favorite kernel even more after discovering its hidden gems of technical design.

## What You Should Know Before Reading This Book

No previous kernel knowledge is necessary, but it helps to have a good understanding of the general concepts of hardware and software. In addition, it helps if you have a working knowledge of the Linux interface and a rudimentary understanding of what’s involved in basic system administration.

It also helps to be able to read C programs, although most of the code provided is explained. For a good introduction to C, I always strongly advise *The C Programming Language*, by Kernighan/Ritchie, the designers of C.

## What This Book Contains

This book begins with an introduction to OS theory and kernel concepts in general and relative to UNIX in detail.

The next chapters are dedicated to the five pillars of every kernel:

- Processes
- Inter-process communication
- Signals (interrupts) handling
- Virtual memory
- File systems

Each chapter is structured the same way; it first gives a detailed explanation of the inner workings of the kernel pertinent to the subject. Then, a few coding examples are provided to show how to change the functionality of the kernel. Finally, the relevant kernel data structures (the C include files) are listed for easy reference. Together with the algorithms listed in the main body of the chapter, the reader has a complete aggregation of code and data, as well as the necessary explanations. There is no attempt to present an exhaustive commentary on the Linux kernel source code, rather we focus on the most important subjects and on performance-relevant issues of the kernel. Appendices are included at the end of the book for system calls, the GPL license, and other useful information.

You can read straight through the chapters to learn more about the Linux kernel, or you might choose to go straight to a chapter of interest and use this book as a reference. Whenever a code snippet is shown in the text, the corresponding data structures can be found at the end of the chapter.

## Where to Find More Information

The most up-to-date information on Linux kernels can be found on the Internet. It is, however, essentially raw data. Gathering this information, assembling it, and putting it into a coherent format is not a trivial task. This is the biggest value of Linux Internals—it provides a coherent, researched, and formatted source of information that is otherwise available to the public through scattered web sites, source code, and articles.

One good source of information on the kernel is, of course, the kernel source code itself. There is a site with an excellent source code navigator for all available architectures and Linux versions at http://lxr.linux.no/source/.

At http://www.linuxhq.com you can find information on all kernel versions, and particularly, on the version currently under development. For a full list of GNU tools, visit www.gnu.org.

Finally, keeping up with the kernel developer mailing list is informative, although the sheer volume of this mailing list and the poor signal-to-noise ratio make it difficult at times to extract any useful information.

## Suggestions, Comments

Any suggestions or comments are very welcome and can be addressed either to moshe_bar@hotmail.com or to Moshe Bar, c/o McGraw-Hill, Professional Book Group, Two Penn Plaza, New York, NY 10121.

## Acknowledgments

First of all, it is my duty to thank God for giving me all I needed to write this book.

This book could not have been done without the help of some star developers of the Linux Kernel Hacking fraternity. People like Ingo Molnar, Andrea Arcangeli, Stephen Tweedie, Hans Reiser, and Steve Best contributed greatly to this book.

Joe Pranevich's article "The Wonderful World of 2.4 Kernels" gave me important ideas on how to generally describe the advances made in the 2.4 kernel. Thank you, Joe.

Matthew Dillon, of FreeBSD fame, wrote an important paper describing general virtual memory concepts that inspired the description of Linux general VM concepts in this book. Thank you, Matt.

A few angels watched over the creation and completion of this book: Patricia Campbell, Scott Fallin, Tom Syroid, Philip Courier and wife Patricia Lambert, and Brad Dixon all voluntarily contributed many hours out of their little available time to help me edit this book. Patricia Campbell and Brad Dixon's technical expertise pointed to many embarrassing mistakes before they found their way to print. Scott Fallin, my long-time partner in the development of a GPL'd Khaos OS, highlighted many difficult to understand text sections and helped me to make them better. Philip Courier and Patricia Lambert, often with a lot of humor, greatly ameliorated the style and consistency of the individual chapters. My friend, author Tom Syroid, helped make this book a reality by sharing his authoring experience with me. To him I am especially indebted.

During the editing process, a mailing list was used (Linux-based, obviously) to discuss topics such as C coding style, the correct definition of terms, etc. among the editors. This proved to be a savvy move and greatly contributed to the spirit of the team and to the quality of this book. Thank you all.

Robo-chan, my soul brother, pushed my spirit up when it was down. Thank you, Roberto.

Many thanks as well to TopTier Israel and the Baan group for providing me with a sysadmin/consultant job during the writing of this book to keep the revenue stream flowing and for providing machinery to test what I write about.

# Chapter 1

## Open Source—Implications for a Modern Operating System

Without doubt, the main reason for the unusual success of Linux is its General Public License (GPL). The concept of Open Source, though, or freeware as it is sometimes called, is actually quite old. The first proponent of freeware was Richard Stallman, of the Free Software Foundation (FSF), who designed the GPL license for some excellent and now-widespread software he wrote—most prominently the Emacs editing environment and the GCC compiler for C and C++. Richard Stallman has also been working for a long while now on a full GNU operating system, a project called GNU Hurd. Under development for nearly a decade, this OS is still not a reality, but the many powerful technologies that have emerged from this project have found their way to other OSs, such as Linux, BSD, and others.

Operating systems benefit from having an Open Source approach to development in two ways: reliability and performance. The reliability of Linux stems in large part from the scrutiny of hundreds of thousands of developers auditing the code, improving it, changing it, and trying it out. As Eric Raymond stated in his famous paper “The Cathedral and the Bazaar,” “Given a large enough beta-tester and co-developer base, almost every problem will be characterized quickly and the fix obvious to someone.”

Linux’ performance benefits much for the same reasons; public scrutiny of the code leads to continuous improvement of the overall efficiency of kernel execution path. Furthermore, many academic institutions have adopted the Linux operating system for their research and have been able to use advanced techniques such as hardware profiling and virtual machine tracers to find hitherto hidden performance bottle-necks in the code.

Finally, through the porting of the Linux kernel to a great variety of processor platforms, certain parts had to be adapted or re-written. Through this process of comparison and adaptation, better code emerged that was soon back-ported to other platforms.

Having so many eyes scrutinizing the Linux code base makes for a better Quality Assurance (QA) department than any closed model software development organization could ever afford. This in turn, makes for better quality software.

A mere development model such as Open Source, cannot by itself replace proper design and coding methods. But here again, the Open Source model excels proprietary models by great lengths. Consider the example of a kernel improvement in Linux. For as long as hackerdom has existed, great emphasis has been put on elegant design, proper data structure design, and performance-related issues. Even in the most hid-
