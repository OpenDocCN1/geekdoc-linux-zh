
Rather than buy a Windows computer and then struggle to obtain a refund, it's generally better to buy a computer with Linux preinstalled, or at least without an OS installed at all. (Many of the small- and mid-sized PC manufacturers will build a computer without an OS installed.) Linux machines are typically harder to find than Windows-based computers, but they're not unobtainable. Chapter 22 covers this topic in more detail.

## Summary

If you're in the market for a new computer, one option is to purchase a machine that was never designed to run Linux, but to run Linux on it anyhow. Most computers can work in this way, although you might have to replace one or two components, such as a software modem or sound card, to get it to work. If you buy a computer from a vendor that will build a system to your specifications, you can ensure that it has adequate hardware from the beginning. You must do some research on basic Linux hardware, particularly video cards, SCSI adapters, and sound cards, if you don't want to be stuck with a machine that runs Linux poorly, if at all.

After you've got your computer, you'll need to spend some time preparing it to run Linux and installing the OS. This task is no different from installing Linux on a system you've had for some time. The task can be safer because, if you make a mistake that wipes out Windows, you can probably recover Windows to its immediate post-installation state by running a recovery CD provided by the computer's manufacturer.

## Linux Workstations

### CHAPTER 22

### IN THIS CHAPTER

- Locating a Linux-Aware Vendor    574
- Evaluating the Hardware    577
- Evaluating the Software    580
- Obtaining Technical Support    583

If you’re in the market for a computer on which you intend to run Linux, the simplest way to ensure hardware compatibility is to purchase the computer from a vendor who sells computers preconfigured with Linux. By doing this, you shift responsibility to the vendor to research specific components, check for strange interactions, and even install Linux in a reasonable way. This can be a great time-saver, although it does have its drawbacks. For instance, if the vendor you select barely understands Linux, that vendor can make mistakes. Letting the dealer configure your Linux system also means that you won’t learn as much about Linux installation and configuration. Finally, you’re likely to pay more for a computer that’s preconfigured with Linux than for an equivalent machine sold with Windows installed. This might seem odd, given that Linux costs less than Windows, but the reason is that you’re paying for a greater level of expertise on the part of the manufacturer. In many cases, Linux computers also contain more expensive hardware than do Windows systems that appear similar at first glance. For instance, many Linux computer dealers use SCSI hard disks, rather than EIDE drives, which both raise the cost and improve performance.

Many of the considerations when you buy a computer preinstalled with Linux are the same as those when you buy a computer that comes preinstalled with Windows. You might therefore want to read Chapter 21, “Store-Bought Non-Linux Systems,” to learn about these issues. I refer to specific sections of Chapter 21 throughout this chapter.

### Locating a Linux-Aware Vendor

If you want to buy a computer with Linux preinstalled, your first challenge is in locating a suitable vendor. At the moment, you’re unlikely to find Linux computers for sale in the local computer superstore, although this could change in the future. Instead, you’ll need to buy through mail order or at a more specialized local store. Locating such sources of supply can be tricky if you don’t know where to look. Fortunately, a few resources can be very helpful in locating Linux-aware computer retailers.

### Major National Computer Companies

There are a few names that consumers associate with new computers: IBM, Compaq, Dell, Gateway, and others. These manufacturers invariably feature Windows on their most popular models, and those are the ones you’ll find on most computer store shelves. Some of these manufacturers, however, offer Linux on some of their computers. These Linux-equipped machines are typically sold as servers, and so have very powerful processors, lots of hard disk space, and other high-end features. If you want a truly well-equipped desktop system, there's no reason you couldn't use one of these "servers" as a workstation. Some specifics include

- **IBM** In 1999 and 2000, IBM dramatically increased its support for Linux, including contributing to some Linux development efforts and porting some of its products to Linux. IBM now offers Linux on some of its Netfinity servers, and has embarked on a program to ensure Linux compatibility for most of its hardware. For more information, check http://www-4.ibm.com/software/ls/mp/linux/.
- **Compaq** Compaq offers Linux as an option on some of its Proliant servers. The company also sells computers based on the Alpha CPU line it acquired from DEC, and Linux is available on some of these computers. For more information, check http://www.compaq.com/products/servers/platforms/ and http://www.digital.com/alphaserver/.
- **Hewlett-Packard** The company best known for its printers also sells computers, and offers Linux on some of its servers. Check http://internetsolutions.enterprise.hp.com/linux/ for more information.
- **Silicon Graphics** Best known for its high-powered UNIX workstations, Silicon Graphics (SGI) offers a line of x86-based Linux workstations as well. You can read more at http://www.sgi.com/servers/1400/lowerview.html.
- **Dell** Dell offers Red Hat Linux preinstalled on a number of its computers. Linux information is scattered about on its Web site; go to http://www.dell.com and do a search on Linux to locate relevant pages.

In most cases, you must purchase these Linux-equipped computers directly from the company, or special-order them through a computer retailer. These models aren't typically on display in local stores. As Linux grows in popularity, though, this might change. Other major computer manufacturers might also begin to offer Linux preinstalled on some of their models.

Large companies that sell Linux as an option typically invest in testing their hardware with Linux, so you can be reasonably sure that the hardware works well with Linux. Some of these companies have invested in Linux driver development or other open source programming projects to further the usability of Linux on their hardware.

One of the biggest advantages of buying from a major non-Linux company is that you have that company's support. This is particularly true if you buy an expensive server system, because such computers often come with good support packages. You can be reasonably certain that a major company like this won't fold any time soon, leaving you with an "orphaned" machine. On the other hand, these manufacturers sometimes use nonstandard hardware, which can be difficult or expensive to upgrade or replace.

### Linux Specialty Vendors

One of your best bets for locating a computer with Linux preinstalled is to purchase from a specialty Linux vendor. These companies specialize in building Linux computers. They can therefore generally be trusted to produce computers that work well under Linux. Most of these companies are small enough that they can't invest in Linux development, but a few, such as VA Linux (http://www.va.linux.com), can do so.

Most Linux specialty stores sell x86-based Linux computers. Some offer Linux installed on other processors in addition to, or instead of, x86 CPUs. The most common non-x86 CPU used is the Compaq (formerly DEC) Alpha CPU, which is very well suited to high-performance computing tasks, particularly those that require heavy floating-point computations. (The special effects for the film *Titanic* were done with a farm of Alpha-based computers running Linux.) Non-x86 computers do have their drawbacks, however, including an inability to run binaries compiled for the more mainstream x86 version of Linux. This fact can be important if you want to run commercial software such as WordPerfect or ApplixWare.

Most Linux specialty stores operate on a mail-order basis. This can make it difficult to evaluate hardware's quality before you buy, but you can still ask some questions to help ensure you get a good product. Read the section "Evaluating Hardware Quality" in Chapter 21 for more information. Of course, if you find a local shop that specializes in Linux, you can check the hardware in person before you buy, which can make buying a good product much easier.

You can find a list of vendors who sell Linux computers at http://www.linux.org/vendors/systems.html. Linux magazines such as *Linux Journal* and *Linux Magazine* also sport ads from these companies. I've listed several of them in Appendix B, under the heading "Computer Manufacturers."

### Local Computer Assemblers

Many small computer shops build computers around a set of hardware choices, but will build a computer to your specifications within that range of hardware. Some will also add one or two custom components; for instance, if you want a specific video board, the store will order it for your computer. Some of these shops are willing to install Linux on a computer, although they usually install Windows.

If you want to buy locally but also want a computer with Linux preinstalled, such local assemblers might be your only choice. The main drawback to such shops is that they might or might not know much about Linux. They therefore might or might not provide optimal hardware for Linux. On the other hand, because they are local, you can go in and examine the hardware yourself before buying it, which is a luxury you don't have in the case of mail-order, specialty Linux retailers.
