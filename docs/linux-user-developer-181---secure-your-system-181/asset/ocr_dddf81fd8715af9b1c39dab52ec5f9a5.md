# OPINION

# The kernel column

Jon Masters summarises the latest happenings in the Linux kernel as Linux 4.12 is released and the merge window opens for what will become Linux 4.13

![](bbox=[0.06, 0.36, 0.24, 0.51])

Jon Masters
is a Linux-kernel hacker who has been working on Linux for more than 22 years, since he first attended university at the age of 13. Jon lives in Cambridge, Massachusetts, and works for a large enterprise Linux vendor, where he is driving the creation of standards for energy-efficient ARM-powered servers.

**L**inus Torvalds announced the release of **Linux 4.12 and in his announcement mail**, he reflected that “4.12 is just plain slow”, noting that this was “one of the bigger releases historically, and I think only 4.9 ends up having had more commits.” And 4.9 was big at least partly because Greg [Kroah-Hartman] announced it was an LTS [long-term support – receiving updates for several years] kernel.” As Linus also says, there’s “nothing particularly odd” that explains the size, just a lot of ongoing development to improve Linux.

A few specific oddities do stand out in the 4.12 diff stats, such as the large number of header files for the newly upstreamed AMD ‘Vega’ graphics support, but aside from that giant change [half of the patchset], other modifications include the usual mix of core kernel, architecture and driver changes typical to any other Linux release.

In pure numbers, Linux 4.12 adds over a million lines of code beyond what was in 4.11 just nine weeks earlier. Linux Weekly News [LWN] has an excellent summary, breaking down the contributions by employers, and by types of developer [those who are paid to those who have no particular affiliation and are doing kernel work in their spare time]. You can find their summary of the make-up of 4.12 at https://lwn.net/Articles/726817.

It may also be interesting to consult the Linux Kernel Newbies summary for detailed patch listings: https://kernelnewbies.org.

The 4.12 kernel includes a number of new features that we have covered in some detail in previous issues. In particular, the support for USB-C means that it will now be possible to use Linux laptops as both a source [power source] and a sink [power consumer] under the control of special drivers that enable the new Power Delivery [PD] features of the latest USB-C protocol. Personally, I’m looking forward to experimenting with ‘topm’ [Type-C Port Manager]. I’m also interested to see the new ‘BFO’ [Budget Fair Queuing] I/O scheduler, which laptop and desktop users might enjoy. The I/O schedulers handle the issuing of I/O operations to disks [such as NVMe solid state drives] and BFO is biased in favour of interactive desktop applications. The I/O schedulers can be set at boot time, and might be set as default on some desktops.

Ted Ts’o has announced the ‘Next steps and plans for the 2017 Maintainer and Kernel Summits’. The Kernel Summit is an annual event during which the core kernel developers gather – and is usually co-located with a Linux Foundation event or the Linux Plumbers Conference, and this year alongside the Foundation’s European Open Source Summit that will take place in Prague – to reflect on how kernel development is going, address burning issues, and ponder certain big goals for the year ahead.

A slightly modified process will be used this year to determine who gets to attend the Kernel Summit. Those with a novel and interesting topic should see http://bit.ly/KSummitDiscuss.

# The merge window cometeth

With the release of 4.12 comes the opening of the ‘merge window’ [period of time – about two weeks – during which disruptive changes are allowed at the beginning of a kernel development cycle] for what will become 4.13. A great many features have already been merged, and at this writing the merge is still in its early days. New features landing in 4.13 will include many behind-the-scenes capabilities that enhance the user experience in subtle ways. These include changes to ACPI to support NV-DIMMs [non-volatile RAM, in particular errors impacting such RAM at run time], a rework of some of the kernel’s handling of NUMA [non-uniform memory access] in servers to address performance regressions that have snuck in since Linux 3.10 days, and many x86 architectural tweaks for servers and laptop systems. Among the latter are patches that [nearly] complete the enabling of Intel 5-level paging [support for 56 bits of memory – a crazy amount in today’s terms], and optimisations for handling process context switches [changing from one running process to another]. Traditionally, when a process switch occurred, it was necessary to signal to all processors which might have been running threads or sharing memory with that process that they should invalidate special internal caches