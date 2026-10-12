The scope of this chapter is forward-looking. Since prebuilt images for the current Red Hat kernels are readily available, and because those ready-made kernels require little more than an `rpm -Uvh` command, your main use of this chapter may be to build the "canonical" Linux kernel from the sources maintained by Linus Torvalds. With Linux in a transition to new release, this chapter will focus on the canonical 2.4 kernel. Because Linux 2.4 is almost twice the size and has four times the configuration options of Linux 2.2, and because your Red Hat kernel will contain some of these features as vendor patches, some descriptions listed here may be slightly different. This chapter can still guide you through a 2.2 install, but it will tend to tease you with features you can only get through the latest sources.

This is also what Red Hat expects you will do with their 7.1 distribution. Most Linux distributions in late 2000 faced the dilemma to include the nearly finished kernel update, or to stay with the tried and true, and very tired, 2.2 kernel. Red Hat chose a middle path and to prepare you for the jump to 2.4, they have already included most of the requisite software and new system configurations that will ease your transition into 2.4.

This chapter is a guide to configuring the Linux kernel for Intel-based computers and will teach you

+   How to obtain and update Linux kernel sources
+   How to compile for multiple machines
+   How to configure modules
+   How to tune virtual memory and filesystem performance using `sysctl`
+   How to add alternate filesystems
+   How to add network services
+   How to add support for special devices such as video/radio/TV cards, joysticks, and infrared controls
+   How to troubleshoot a new kernel

Don't expect to do everything at once. You may only need to consult those few sections on installing your sound or network device. On the other hand, for difficult kernel optimization, advanced networking, or tailoring the kernel for embedded and other special situations, this chapter should give you an overview of what is possible.

# Introduction to the Linux Kernel

You may think kernel tuning is no place for the average user. This is both true and false. Like other features of Linux, the possibilities are endless and deep, but you don't need to understand all the gory details of PCI chipsets to tailor a better Linux for your computer.