# # Installation

This chapter provides an overview of how to install a Linux system on a PC with an Intel-compatible processor. It does not refer to a particular distribution, but describes the relevant installation steps (such as partitioning the hard disk) in a general way and conveys the necessary basic knowledge (so that you know what you are doing). Specific details of some selected distributions can be found in Appendices A to C.

The most tiresome but most cases unavoidable step in a first installation of Linux is repartitioning the hard disk. In the course of this chapter, the necessary commands (FDISK and FORMAT under DOS, disk under Linux) are described in detail. This chapter also explains the installation of Umsdk, which avoids repartitioning (but has several other disadvantages).

So much for starters: during recent years, installation has become increasingly simple. Many detailed problems described in this chapter refer to older hardware, which by now only seldom used!

In this chapter, both DOS and Linux commands appear. Some of these commands have the same name (disk!). For this reason, Linux commands are shown in small letters (and under Linux they must be entered this way), whereas DOS commands are given in capitals (although in DOS it does not matter whether commands are entered in upper or lower case letters).

# ## 2.1 Requirements

In order to be able to install Linux, several requirements must be met:

+   - You need a PC with an Intel 386-compatible processor. (There are Linux distributions for systems with other processors, but this book does not deal with them.)