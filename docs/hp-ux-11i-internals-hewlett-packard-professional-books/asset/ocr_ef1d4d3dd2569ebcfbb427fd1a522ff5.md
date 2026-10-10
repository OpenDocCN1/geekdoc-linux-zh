# CHAPTER 8

# # Files and File Systems

T he file system is a basic workhorse component of an operating system. Figure 8-1 shows the big picture of the file management subsystem in the HP-UX kernel. Our study is divided into three phases: first we examine basic file system concepts, then we focus on the design and implementation of the classic UNIX File System (UFS), and finally we examine the kernel-resident structures utilized to keep track of mounted file systems.

![](bbox=[0.25, 0.5, 0.85, 0.85])

**Figure 8-1** The File Management Subsystem