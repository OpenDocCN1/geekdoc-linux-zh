# Linux Administration: A Beginner's Guide

and eventually reaches full refinement. This fully refined program contains contributions from possibly hundreds if not thousands of programmers who have added little pieces here and there. In fact, the original author's code is likely to be little in evidence.

Here's another reason for the success of generally licensed software: Any project manager who has worked on commercial software knows that the real cost of developing software isn't in the development phase. It's really in the cost of selling, marketing, supporting, documenting, packaging, and shipping that software. A programmer carrying out a weekend lurk to fix a problem with a tiny, kludged program can neither the interest, time, nor backing money to turn that hack into a profitable product.

When Linus Torvalds released Linux, he released it under the GPL. As a result of his open character, Linux has had a notable number of contributors and analysts. This participation has made Linux very strong and rich in features. Torvalds himself estimates that since the v 2.2.0 kernel, his contributions represent only 5% of the total code base. Some people have made money with Linux, since anyone can take the Linux kernel (and other supporting programs), repackage them and resell them. As long as these individuals release the kernel's full source code along with their individual packages, and as long as the packages are protected under the GPL, everything is legal. This of course means that packages released under the GPL can be resold by other people under other names for a profit.

In the end, what makes a package from one person more valuable than something from another person are the value-added features, support channels, and documentation. Even IBM can agree to this; it's how they made a bulk of their money between the 1930s and 1970s: The money isn't in the product, it's in the services that go with it.

# THE MAJOR DIFFERENCES BETWEEN NT AND LINUX

As you might imagine, the differences between Microsoft Windows NT and the Linux operating systems cannot be completely discussed in the confines of this section. Throughout these chapters, topic by topic, we'll examine the specific contrasts between the two systems. In some chapters, you'll find that we don't derive any comparisons because a major difference doesn't really exist.

But before we attack the details, let's take a moment to discuss the primary architectural differences between the two operating systems.

# Single-User vs. Multi-User vs. Network User

Windows NT was designed according to the vision of Microsoft's cofounder Bill Gates: one computer, one disk, one user. For the sake of discussion, we'll call this philosophy single-user. In this arrangement, two people cannot work in parallel running (for example) Microsoft Word on the same machine at the same time. (On the other hand, one might question the wisdom of doing this with an overwhelmingly weighty program like Word!) Linux borrows its philosophy from UNIX. When UNIX was originally developed at Bell Labs in the early 1970s, it existed on a PDP-7 computer that needed to be shared amongst an entire department. It required a design that allowed for *multiple users* to log