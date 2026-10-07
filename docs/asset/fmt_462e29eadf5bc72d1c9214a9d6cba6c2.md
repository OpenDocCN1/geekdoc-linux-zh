
# Dragonfly BSD 讨论记录

**MD:** I think open source in general needs a bit of a risk. I think of open source programmers who didn't have the benefit of the early Wild West era of Linux. In modern times, projects tend to be much, much larger, and no single programmer can write or maintain it. The open source model for a project often does not fit it anymore, or at least, not see significant effect after the early authors move to other pastures. People want to work on big hunt somebody else's project – there is a little recognition in such endeavors. The GNU license while being up a ball and chain as it opens up code to the wider world, is not a ball and chain. The more realistic BSD-give-away of life Linux became dominant.

Note: Due to the provided OCR text having significant repetitions and fragmented sections, I have provided the coherent de-duplicated version of the narrative flow.

Ultimately the BSD projects' problems caused them to lose, and younger generations became enamored with GNU licensing whereas the more realistic BSD-give-away of life; Linux became dominant.

The connection (stream or packet-combination) just as close to likeness as it is possible to go.

typical independent backup and snapshotting mode:

The Dragon-subsystems are quite like Linux, so we get some users to come into FreeBSD from other operating systems for specific domains. Among these is strong freedom on machines with limited amounts of RAM and a really excellent process selector. Our swap and paging system is one of the best of all and can run on low-memory machines and still give users an excellent experience (even when they tabs open for weeks, which takes a lot of space besides memory leaks).

## LM: Why was Dragonfly forked?

Over time, Linux, Dragon, and FreeBSD all came to nearly the same place. Not that the Linux focuses more on performance, but its mechanisms are considerably more fragile than Dragon focuses on a combination of SMP, stability, and flexibility. FreeBSD is similar. All of the projects have to compile the build of third-party applications that end up there. In short, Linux is ahead of Dragonfly on drivers (mostly), but at the raw level all projects share a great deal of intellectual conversation, and benefit. That's the reality of how all of them work.

## MD: Dragonfly BSD was forked off for several reasons.

Personal interactions coupled with secrecy and backdoors caused the mailing lists of the FreeBSD project to become toxic (before, and after them). A great deal of resistance to rising up and rewriting subsystems multiple CPUs became more popular than wanting their opinions heard, but few of them were actually doing that the combination was falling out, so the project and Dragonfly was forked.

FreeBSD ultimately went a more conservative path kept it in the game, and many of its principles were able to put together small businesses or to work for large businesses (for example, Netflix) near their project.

## LM: What do users find in Dragonfly BSD?

A BSD user would find a complete base system installation that might not be taken at the cost of giving hardware support. FreeBSD changes all the time, is mostly proprietary, and requires a lot of effort to reverse engines. Linux has the BSDs to reverse.

The Dragonfly project was more maintained than its open source/social roots, remaining so to that day. Other BSDs exist to today, but to be completely honest all the BSD projects have been gone out slowly, and the Linux offers a similar path, at a much larger scale.

## LM: What are Dragonfly's distinguishing features? What do we think?

## MD:

It is a very special project so we mostly talk about it these days, with mailing lists for announcements. The social atmosphere has been quite laid bad. It's very nontoxic, if anyone. Generally, if someone wants to do a particular piece of work, they are really in the driver's seat to see how it should be done. The rest of the system is to help and make sure that the code is up to standards by actually working the cooperatively back and forth, not just putting ideas out on mailing lists. We do have at a co-location and so some

## LM: How is Dragonfly BSD organized and governed?

Our focus was on symmetric multiprocessing (SMP) locked as much as possible. Our note is that the Linux SMP lock is the one you don't need to have in the first place. We focused on partitioning the CPUs to remove locking entirely. Of course, there is a lot of locking. There are still shared resources. But Dragonfly has a number of subsystems lockless, as the network protocol stacks and packet files. Not just lockless, but completely unshared, so the Ethernet hardware-Topoplaz hash a packet directly to the correct CPU and the network stack on it operates

## MD: Are there any distinguishing features that beyond ephemeral stability, performance, and filesystems.

So we have MERGE2, which is an excellent image-file system, but we have taken on block-level redundancy mechanisms. On the other hand, most users abuse such mechanisms and wind up with less stability than they would just using a significant process power for driving bulk builds and such. interms means. All DragonFly have their own lives ... the project does not require 24x7 attention. successful its open source makes exploitation too easy (just by a project) involving many contributors at a large company vs being contained to a single person. A great deal of the spirit has been lost.

## LM: Do you have any statistics about liking regular contributors and the number of users?

## MD: Would you like to say anything else?

Open source programmers, for the most part, have to make their livelihoods in other ways – either leveraging the experience to obtain a good job, or by some other means even related to the original work. It is not a failure, as because open source has created a technological baseline for the world – a very very high bar for commercial coding otherwise society with junk. It is perhaps, not really today's open source authors were hoping for.

## MD: Regular contributors are one or two or so: I don't know about others, but I am constantly surprised by the number of emails I get from people using the system.

## MD: I think open source in general needs a bit of a risk. I think of open source programmers who didn't have the benefit of the early Wild West era of Linux. In modern times, projects tend to be much, much larger, and no single programmer can write or maintain it. The open source model for a project often does not fit it anymore, or at least, not see significant effect after the early authors move to other pastures. People want to work on big hunt somebody else's project – there is a little recognition in such endeavors. The GNU license while being up a ball and chain as it opens up code to the wider world, is not a ball and chain. The more realistic BSD-give-away of life Linux became dominant.

---
**注：由于提供的 OCR 文本包含大量的重复和片段，我已为您提供了连贯的去重翻译。**

以下是翻译后的中文内容：

最终，BSD 项目的问题导致了它们的失败，年轻一代开始迷恋 GNU 许可协议，而选择了更现实的 BSD 式生活馈赠；Linux 占据了主导地位。

这种连接（流或数据包组合）已经尽可能达到了相似的程度。

典型的独立备份和快照模式：

Dragon 子系统与 Linux 非常相似，因此我们有一些来自其他操作系统的用户为了特定领域进入 FreeBSD。其中包括在内存有限的机器上具有强大的自由度，并拥有一个非常出色的进程调度器。我们的交换和分页系统是所有系统中的最优之一，可以在低内存机器上运行并为用户提供极佳的体验（即使 Chrome 标签页打开了几周，除了内存泄漏外，也会占用大量空间）。

### LM: 为什么 Dragonfly 会分支（fork）？

随着时间的推移，Linux、Dragon 和 FreeBSD 都走向了几乎相同的终点。并不是说 Linux 更关注性能，而是它的机制比 Dragon 更加脆弱，而 Dragon 则专注于 SMP、稳定性和灵活性的结合。FreeBSD 也是如此。所有项目都必须编译运行在在那里的第三方应用程序构建。简而言之，Linux 在驱动程序方面（大部分）领先于 Dragonfly，但在原始层面，所有项目都共享大量的智力交流并从中受益。这就是它们所有运行方式的现实。
