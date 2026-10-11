
# THE OPEN SOFTWARE COLUMN

### Should the world be appier?

Simon asks whether Apple’s creation of an ‘app’ culture is good for software

![](img/daaca9116bc2b1db669c224de81abc7c_10_0.png)

**Simon Brew** is a technology writer and editor, working across the Linux, Windows and Mac OSX platforms

![](img/daaca9116bc2b1db669c224de81abc7c_10_1.png)

Right! Apple managed to reinigorate the computer program for the modern age with its App Store.

Apple-ﬁcation isn’t really a word, and I’m not going to pretend otherwise. But it is something that increasingly (and badly) describes how computer products and software are being described. In particular, Apple has taken the word ‘app’ (which is now a standard word), and it’s being exchanged with the old fashioned way of describing things, as computer programs. We’re not even allowed to call them ‘applications’ any more under this new world order.

Apple’s marketing savvy is the subject of exhaustive books and endless PowerPoint presentations, but it’s interesting what it’s achieved. Who, after all, describes an iPad as a computer? A mobile phone has been exchanged for the shorthand of iPhone, and the injecting of a lower case letter ‘i’ before any other word seems to be the foundation of many a major product launch now. Heck, I might start calling this an iColumn and sending in an invoice for double the amount. It’s worth a try.

What’s interesting is that Apple’s ideology (in both user interface and proprietary tech) is moving beyond the core technology with which it’s usually associated. For instance, I’ve recently bought a new television. It’s always fun getting one, especially as I’m one of those old duffers who likes to buy a new telly and then keep it for the best part of a decade (in an old fashioned approach, granted). I noticed, on unpacking it all, that I appeared to have an ‘App’ button on my new remote control, and duly pressed it once the set was up and running. And as you might expect, a screen popped up, listing a collection of installed applications, and inviting me to go to whatever the manufacturer concerned had called its ‘App Store’, getting as close as possible without attracting a letter from Apple’s legal department. An IT threat, no doubt.

It’s easy to sneer at the proliferation of the ‘App’ culture, that has taken bloated computer programs in some cases and boiled them down to individual tasks, no least because most of the options on my new telly are plain tat. Still, if you look at the history of the PC, budget publisher Cosmos made a living for a while by effectively cutting up the functionality of Microsoft Oﬃce into chunks, and selling software that took it at a time. So, a business card designer, or a labels product. You more than likely had the features already, but there’s something inherently more simple about having one tool for one job, rather than a big suite to encompass lots of things.

What Apple has managed to do, and what open source software also embraces from time to time, is to put all that into a package that sounds attractive, non-techy and accessible. Many ﬁrms beforehand did the technological pathﬁnding that Apple stands on the shoulders of, and many now stand on the shoulders of Apple itself. But few have worked out how to package it all together in quite as appealing a way.

It’s a shame, because there’s not a tool that Apple oﬀers for which a competent-to-brilliant open source alternative doesn’t exist. But quality doesn’t necessarily bubble to the top, especially when most people ﬁnd their ‘app’ by a search rather than a browse in a physical store. As such, and it goes against some of the ethos of why many get into open source in the ﬁrst place, maybe a drop of Apple inﬂuence in some regards, if not Apple behaviour, might just be of us.

# The kernel column

Jon Masters summarises the latest happenings in the Linux kernel community, beginning with the just-released 3.16 kernel

![](img/daaca9116bc2b1db669c224de81abc7c_11_0.png)

**Jon Masters** is a Linux kernel hacker who has been working on Linux for some 19 years, since he first attended university at the age of 15. Jon lives in Cambridge, Massachusetts, and works for a large enterprise Linux vendor. He publishes a daily Linux kernel mailing list summary at kernel@podcast.org

As we were going to press, Linus Torvalds announced the 3.16 Linux kernel, saying “So nothing particularly exciting happened this week [since the final 3.16 Release Candidate 7 from a week prior], and 3.16 is out there.” In his announcement email, Linus noted that the timing of 3.16 was, perhaps, a little unfortunate for the impact upon the merge window for 3.17. The “merge window” is the period of time early in a (roughly) two month kernel development cycle during which disruptive kernel changes are allowed to take place. Typically, the merge window is capped at a couple of weeks, and it immediately follows a final release (from the previous kernel development cycle). Therefore, the merge for 3.17 is open just as Linus (and others) are preparing to head to Chicago for the 2014 Kernel Summit (and LinuxCon conference). Linus says, “So we’ll see how the next merge window goes, but I’m not going to worry about it overmuch. If I end up not having time to do all the merges, I might delay things into the week of the Kernel Summit, but I’ll hope to get most of the big merge done this upcoming week before any travel takes place.”

Linux had been concerned for a few weeks that Linux 3.16 “looked a bit iffy for a while,” chiefly because of the amount of late-in-cycle code churn that was taking place. By the time we got to 3.16-rc6, Linux was sounding the alarm, saying “Week by week, we’re getting to what is supposed to be the last rc, but, quite frankly, things aren’t calming down the way they are supposed to.” He then noted how RC5 had been larger than RC4, and RC6 was still larger than RC5 had been. “That’s not how this is all supposed to work,” said Linus. Nevertheless, by the time 3.16 final rolled around, Linus was less alarmed and thought that things had “cleared up nicely,” just as he was beginning to fear that additional stabilising RCs might have been (unusually) necessary. It is possible that this will combine with the fears around a merge window for 3.17 happening during Kernel Summit to mean that it is even more cautious in this next merge cycle around such churn.

Linux 3.16 brings with it a number of new features. Unlike in many recent development cycles, these new features are more “internal” – and aimed towards developers – than they are new earth-shattering features for end users. For example, the kernels’ earlyprintk diagnostic output support has been reworked into the newly generic “earlycon” interface, and a number of block I/O subsystem components have been moved into the kernel’s code/ directory (to more clearly show maintainership, with only a few changes to the code itself). End user visible changes of note include support for UEFI boot firmware on the ARM64 (Arch64) 64-bit ARM Architecture, which will be particularly important for the coming wave of industry standard ARM servers, which will all boot using this method.

### Early kernel logging

The newly reworked “earlycon” kernel mechanism in 3.16 generalises the existing in-kernel “earlyprintk” mechanism across architectures. Early printc is a mechanism that allows the kernel to output diagnostic information (including the famous kernel_banner that includes the version number) early during the boot process, before the regular facilities for kernel logging have fully come online. Historically, each architecture implemented things a little differently. For example, the 64-bit ARM Architecture – known as arm64 to the kernel – used a simple driver that was registered during early_param parsing within the kernel boot cycle (after running setup_arch, but before doing a lot more than getting the basic Virtual Memory subsystem up and running). The ARM kernel would look for a kernel command line option of “early_printk=” that would include the address of a serial port UART controller, as well as its type, to which the kernel would log messages before it had properly initialised its serial console.

Those booting without special early_printk options would still get to see boot messages, but they would be buffered and displayed later in the boot process, once the standard infrastructure for logging was online. The user would unlikely notice the difference as many systems don’t display these messages by default, and the buffering would only delay output by less than a second in any case, but during that crucial second, many other things could have gone wrong that kernel developers would care about in debugging critical kernel issues. The new debug infrastructure for diagnostic logging is known as “earlycon” and it replaces the boot parameter with the same name. As an aside, specifications such as ACPI allow for a diagnostic console to be defined by a system vendor, and it is hoped that systems such as PCs will be able to automatically use this information in the future.
