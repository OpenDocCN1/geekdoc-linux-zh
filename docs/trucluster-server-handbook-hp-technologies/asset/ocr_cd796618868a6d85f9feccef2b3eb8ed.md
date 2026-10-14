# ## *Tru64* UNIX & *TruCluster* Server Overview

Before diving into the world of designing and configuring a *Tru64* UNIX cluster, a brief overview of the *Tru64* UNIX operating system will help set the table. Consider this chapter the appetizer, and the following chapters as the main meal. To enable you to digest the main topics in this book, we will prepare you by discussing several concepts and features of *Tru64* UNIX and the *TruCluster* Server software that is now part of the operating system.

# ### 2.1  *Tru64* UNIX Overview

The name of this operating system speaks volumes. First, it is a UNIX-based operating system. It falls towards the middle of the UNIX family tree because it draws some of its characteristics from both the BSD¹ and System V² sides of the family. It also has a healthy dose of core code created by Compaq engineers.

Figure 2-1 depicts several of the common UNIX variants. Note *Tru64* UNIX at the bottom of the diagram.

Second, *Tru64* Unix is truly a 64-bit operating system. The virtual addresses used in the system are indeed 64 bits, providing a huge virtual address space and supporting large file offsets and sizes. So, is that it? Are those the distinguishing features of the system? There are actually many more features of the operating system which we will visit in the first part of this chapter. If you are familiar with another UNIX system, you may want to take a quick look at the first section of this chapter but plan on slowing down and carefully reading the *TruCluster* Server Overview (section 2.7).

¹ Berkeley Standard Distribution (BSD), developed at the University of California at Berkeley.
² UNIX System V, developed by the UNIX System Development Lab at AT&T.