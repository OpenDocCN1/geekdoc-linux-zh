To get a better feel for patch files, have a look at one or more of the files under the patches/ subdirectory. Try, for example, arm/0001-deb-pkg-Simplify-architecture-matching-for-cross-bui.patch. This happens to be a patch to a shell script.

# The Kernel Source Tree

Needless to say, the kernel encompasses a very large number of files—C sources, headers, makefiles, scripts, etc. The BeagleBone version 3.8.13 kernel has 48,683 files, taking up 1.7 GB. So, not surprisingly, there is a standard directory structure to organize these files in a manageable fashion. Fig. 12.3 shows the kernel source tree starting at kernel/kernel/. The directories are as follows:

.git — This hidden folder is not part of the kernel source, but rather has to do with git.

Documentation — Pretty much self-explanatory. This is a collection of text files describing various aspects of the kernel, problems, “gotchas,” and so on. There are many subdirectories under Documentation/ for topics that require more extensive explanations. While the information here is generally useful, it also tends to be dated. That is, the documentation was initially written when a particular feature was added to the kernel, but it has not been kept up as the feature has evolved.

arch — All architecture-dependent code is contained in subdirectories of arch. Each architecture supported by the kernel has a directory under arch/ with its own subdirectory structure. The executable kernel image will end up in arch/<architecture>/boot. An environment variable in the makefile, ARCH, points to the appropriate target architecture directory. arch/ is one of the two largest subtrees in the kernel, comprising just over 15,000 files.

block — The block layer. This is the code that optimizes transfers with block storage devices.

crypto — Code dealing with the cryptographic aspects of system security.

drivers — Device driver code. Under drivers is a large number of subdirectories for various devices and classes of device. This is the other major kernel subtree, with over 14,000 files.

firmware — Binary firmware files for devices that load firmware at boot time. Ultimately these files are to be moved to User Space, because they are, for the most part, proprietary and mixing them with the GPL’ed kernel code is “problematic.”

fs — File systems. Under fs is a set of directories for each type of file system that Linux supports.

include — Header files. The most important subdirectory of include/ is linux/, that contains headers for the kernel APIs.