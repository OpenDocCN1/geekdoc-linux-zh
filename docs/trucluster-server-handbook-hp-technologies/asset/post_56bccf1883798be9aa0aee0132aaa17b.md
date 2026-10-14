
## 1.5 What This Book Covers

We will cover a great deal of material in this book, but there are some topics that will not be covered. For instance, while we are aware of various techniques in which to deploy Stretch Clusters and Disaster Tolerant (DT) Clusters, at this time, it is neither recommended nor generally supported by Compaq. We will also not cover Compaq’s AlphaServer SC Supercomputer implementation in this book because the subject would encompass an entire book on its own.

When we decided to write this book, it was and continues to be our goal to provide a comprehensive technical guide that can be used to design, implement, deploy, and administer a TruCluster Server environment. We also wanted to remove the mystery and "magic" from what a UNIX Cluster is and why IT managers may want to use this technology to help them decrease their overall systems management costs while increasing manageability and availability of their UNIX server infrastructure. To that end, we have organized the book into ten sections and an appendix for easy reference.

- Section 1 - This is the Introduction and provides a certain amount of background on UNIX clustering and a good overview on Tru64 UNIX and TruCluster Server. For folks not familiar with UNIX clustering and/or Compaq’s Tru64 UNIX, we strongly recommend that you start with this section as it lays the foundation for more to come.
- Section 2 - This section is on Design and Configuration of a Tru64 UNIX Cluster is a very important section as it discusses the design, planning, and configuration of a TruCluster Server environment. We recommend that before you even think about the mechanics of deploying Tru64 UNIX for a TruCluster Server environment, you first design and carefully plan out your environment. As with most endeavors, a little up front design and planning will save you a lot of work in the long run.
- Section 3 - This section provides information on how to build and configure Tru64 UNIX in preparation for installing and configuring TruCluster Server.
- Section 4 - Cluster Hooks covers those features in the Tru64 UNIX operating system that are the enablers for clustering. This section provides the background to understanding the basis for what is needed in the operating system to allow for clustering on UNIX.
- Sections 5 & 6 - The actual planning, installation, and deployment of a TruCluster Server environment. This section should be especially useful to systems architects and systems administrators.

## Tru64 UNIX & TruCluster Server Overview

Before diving into the world of designing and configuring a Tru64 UNIX cluster, a brief overview of the Tru64 UNIX operating system will help set the table. Consider this chapter the appetizer, and the following chapters as the main meal. To enable you to digest the main topics in this book, we will prepare you by discussing several concepts and features of Tru64 UNIX and the TruCluster Server software that is now part of the operating system.

### 2.1 Tru64 UNIX Overview

The name of this operating system speaks volumes. First, it is a UNIX-based operating system. It falls towards the middle of the UNIX family tree because it draws some of its characteristics from both the BSD¹ and System V² sides of the family. It also has a healthy dose of core code created by Compaq engineers.

Figure 2-1 depicts several of the common UNIX variants. Note Tru64 UNIX at the bottom of the diagram.

Second, Tru64 Unix is truly a 64-bit operating system. The virtual addresses used in the system are indeed 64 bits, providing a huge virtual address space and supporting large file offsets and sizes. So, is that it? Are those the distinguishing features of the system? There are actually many more features of the operating system which we will visit in the first part of this chapter. If you are familiar with another UNIX system, you may want to take a quick look at the first section of this chapter but plan on slowing down and carefully reading the TruCluster Server Overview (section 2.7).

¹ Berkeley Standard Distribution (BSD), developed at the University of California at Berkeley.
² UNIX System V, developed by the UNIX System Development Lab at AT&T.
