# Why You Might Need This Chapter

First of all, kernel configuration is interesting, and an understanding of the process is useful. You may have much occasion to rebuild the kernel provided by SUSE in order to make an unusual configuration change to get support for experimental or unusual features that are not allowed in the default configuration.

You might want to experiment with creating a monolithic kernel supporting the exact hardware on your system without loading anything as a module (although, as noted previously, this will not have a serious effect on performance).

You also might want to experiment with functionality that is available only in the form of kernel patches; to do this, you will first need to patch the kernel source and then rebuild it.

But it is only in unusual cases that you will need to put most of this into practice; usually the work has been done for you by the nice people at SUSE. Note that SUSE always provides experimental kernels as RPM packages (the "kernel of the day”).

# SUSE Kernels and Vanilla Kernels

Traditionally, the kernels shipped by SUSE and other commercial Linux vendors have always differed from the official kernels (often known as vanilla kernels) that are available from www.kernel.org. Exactly how much difference has there been varied with time. During the long period when the 2.4 kernel series was the stable kernel and extensive development was being done on the 2.5, a large number of 2.5 features were backported into SUSE's 2.4 kernels. The 2.4 kernels with various backported features were standard for a long time until version 9.0 Professional and SUSE Linux Enterprise (SLES) 8.

The first release of the 2.6 kernel was in December 2003. SUSE moved to the 2.6 kernel with the SUSE Linux 9.1 release and SLES 9. Current SUSE kernels still contain a significant number of specific patches added by the SUSE team.

SUSE Linux versions 9.0 and SLES 8, SUSE Linux OpenExchange Server (SLOX), and Standard Server 8 use 2.4 kernels.

# Kernel Version Numbers

A Linux kernel has a version number like 2.6.12.4 (the latest stable version of the kernel at the time of this writing). The convention is that the stable kernel has a middle number that is even. Thus 2.0, 2.2, 2.4, and 2.6 are successive stable kernel series. The odd numbers represent the development series: For a long