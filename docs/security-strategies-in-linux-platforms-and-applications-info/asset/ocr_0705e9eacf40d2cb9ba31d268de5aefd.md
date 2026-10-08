# 288 PART 2 | Layered Security and Linux

The first release of an update version kernel has three numbers, as which 2.6.32. The first patch of update version is release 2.6.32.1.

The numbering system for the stock kernel varies slightly from that built for many major distributions. The developers behind a distribution incorporate bug fixes and security updates on their. Therefore, they leave the fourth number associated with such bugs and security.

The developers behind some of the most important distributions may release their enterprise-ready distributions with slightly older kernels. That supports a longer period of testing with a stable kernel. When new features are incorporated into later kernels, the developers behind any Linux distributions may backport features. For example, Red developers have backported features associated with kernels 2.6.19–2.6.33 into its build of the 2.6.18 kernel for its Red Hat Enterprise Linux releases.

# Production Releases and More

The developers associated with the Linux Kernel Organization maintain production kernels associated with multiple update numbers. When administrators build a kernel to a certain update version, they may choose to stick to that update version for a while so they do not test their systems for compatibility with the new features associated with later updates.

Linux kernel release security patches for a number of different kernel update versions. For example, as of this writing, stable security patches are available for Linux kernel number 2.6.33, 2.6.32, 2.6.27, and 2.4.37.

The Linux Kernel Organization releases more than just kernels. Developers test kernels in work. Kernels associated with a development branch are frequently associated with chief developers; for example, a kernel with a -ac suffix is associated with Alan Cox. Kernels that are nearly ready for release may have a -rc suffix, indicating they are a candidate release.

Generally, if there's an important security issue, it is most efficient to wait for the latest production release. Security issues get special attention not only by the Linux Kernel Organization, but also by the developers behind major Linux distributions.

# Download the Stock Kernel

To use a Linux kernel, start with the version available from the Linux Kernel Organization at http://kernel.org. You may choose to start with the latest stable kernel or some older kernel that is still maintained. The stock kernel is available as source code. Before it can be put into effect on a system, it must be compiled, as discussed later in this chapter.

Stock kernels are normally available in a compressed command archive. compressed either with the Lempel-Ziv Gzip or the Burrows-Wheeler block sorting compression algorithm with Huffman coding. Kernels compressed in these formats have .tar.gz and .tar.bz extensions, respectively.