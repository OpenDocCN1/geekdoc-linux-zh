# # Chapter 14. Block Drivers

# ## In This Chapter

+   - **Storage Technologies** 416
+   - **Linux Block I/O Layer** 421
+   - **I/O Schedulers** 422
+   - **Block Driver Data Structures and Methods** 423
+   - **Device Example: Simple Storage Controller** 426
+   - **Advanced Topics** 434
+   - **Debugging** 436
+   - **Looking at the Sources** 437

Block devices are storage media capable of random access. Unlike character devices, block devices can hold filesystem data. In this chapter, let’s find out how Linux supports storage buses and devices.

# ## Storage Technologies

Let’s start by taking a tour of the popular storage technologies found in today’s computer systems. We’ll also associate these technologies with the corresponding device driver subsystems in the kernel source tree.

*Integrated Drive Electronics* (IDE) is the common storage interface technology used in the PC environment. ATA (short for *Advanced Technology Attachment*) is the official name for the related specifications. The IDE/ATA