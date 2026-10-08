
## 288 PART 2 | Layered Security and Linux

The first release of an update version kernel has three numbers, such as 2.6.32. The first patch of an update version is release 2.6.32.1.

The numbering system for the stock kernel varies slightly from that built for many distributions. The developers behind a distribution incorporate bug fixes and security updates on their. Therefore, they leave the fourth number associated with such bugs. Some of the most important distributions may release enterprise-ready kernels that supports a longer period of testing with a stable kernel. When new features are incorporated into later kernels, any Linux distributions may backport features. For example, developers have backported features with kernels 2.6.19–2.6.33 into its build of 2.6.18 for Red Hat Enterprise releases.

## Production Releases and More

The developers behind the Linux Kernel Organization maintain production kernels with multiple update numbers. When administrators build a kernel to a certain update version, they may choose to stick to that update version for a while so they do not test their systems for compatibility with new features. Linux kernel release security patches for different kernel versions. For example, as of this writing, stable security patches are available for Linux kernel 2.6.33, 2.6.32, 2.6.27, and 2.4.37.

The Linux Kernel Organization releases more than just kernels. Developers test kernels in a development branch; for example, a kernel with a -ac suffix is associated with Alan Cox. Kernels that are nearly ready for release may have a -rc suffix, indicating they are candidate release. Generally, if there is an important security issue, it is most efficient to wait for the latest production release. Security issues get special attention not only by the Linux Kernel Organization but also by the major Linux distributions.

## Download the Stock Kernel

To use a Linux kernel, start with the version available from the Linux Kernel at http://kernel.org. You may choose the latest stable kernel or some older kernel that is still maintained. The stock kernel is available as source code. Before it can be put into effect on a system, it must be compiled, as discussed later in this chapter. Stock kernels are normally available in compressed archive compressed with Lempel-Ziv Gzip or Burrows-Wheeler block sorting algorithm with Huffman coding. Kernels compressed in these formats have .tar.gz and .tar.bz extensions, respectively.

## CHAPTER 10 | Kernel Security

 289

You can download the compressed source kernels from http://www.kernel.org/pub/ or ftp://ftp.kernel.org/pub/. Kernel packages should be downloaded to the /usr/src/ directory.

If you have doubts about the integrity of the source code, download the associated compressed archive with the .sig extension. For example, if you downloaded the linux-2.6.34.1.tar.gz file, you can also download the linux-2.6.34.1.tar.gz.sig file. Instructions associated with this signature are available at http://www.kernel.org/signature.html.

Once downloaded, the source code can be unpacked into a subdirectory similar to one of the following commands. Substitute the version number of the downloaded Linux kernel for 2.6.34.1:

```bash
# tar xzf linux-2.6.34.1.tar.gz
# tar xf linux-2.6.34.1.tar.bz2
```

The tar command is one of those rare Linux commands where there is no dash in front of command switches. The z uncompresses .tar.gz files; the j uncompresses .tar.bz files.

If you need to know more about the changes made to produce a production kernel, download the Changelog file associated with the release version.

## Stock Kernel Patches and Upgrades

If a downloaded, unpacked and unarchived stock kernel is available in an appropriate directory, you don't need to repeat the process for the next release. All you need to do is download the source code and the appropriate patch. Different types of patches are available. For example, to update source code from version 2.6.34.1 to 2.6.34.2, the appropriate patch is available in the package named patch-2.6.34.2.gz or patch-2.6.34.2.bz2. Once copied to the /usr/src/ directory, you can apply the patch with one of the following commands:

```bash
# zcat patch-2.6.34.2.gz | patch -p0
# bzcat patch-2.6.34.2.bz2 | patch -p0
```

It's also possible to patch kernel source code between update versions. For example, the patch-2.6.35.gz file can be used to update Linux kernel source code from version 2.6.34. However, patches can be applied only consecutively. For example, to update source code from 2.6.33 to 2.6.35, you would need to apply both the patch-2.6.34.gz and patch-2.6.35 updates.

> TIP
> It's generally a bad idea to use a generic patch on kernel source released for a specific distribution. For example, the source code for the latest Red Hat Enterprise 5 kernels includes backports from the latest kernel releases. A patch applied to that source code might overwrite those backports, removing features that you may need.

## Security and Kernel Update Issues

Kernel can be divided into two interrelated areas. First, there are security issues that arise from the stock Linux kernel. Second, there are security issues that arise related to the Linux kernel as built by the developers of a distribution.

When updating a kernel, it's best to make sure that any working kernel is retained on your system. If there is a problem with the updated kernel, those systems will still be bootable and available with the older kernel. In general, it's easiest to put into effect the binary kernels built by the developers of a distribution. Because such kernels are in binary format, you do not need to compile them.

However, custom kernels work better for many systems. Most importantly, custom kernels can exclude options that may be loaded by hackers.

## Stock Security Issues

The developers associated with the Linux kernel communicate primarily by messages on mailing lists. To keep up to date with the latest developments in the kernel navigate to http://lkml.org/ the kernel mailing list. But it's time-consuming to monitor this list, as there are frequent hundreds of messages between developers on a daily basis.

One more focused on generic security issues is available at http://www.linuxsecurity.com/. For digest of information, see the latest Linux advisory available from that Web site. For many administrators, distribution-specific security monitors may be more active, and are discussed in Chapter 11.

Linux kernel developers can't test updates against all configurations. Any updates they create may lead to problems. So it's important to test all kernels before installing them on production systems. This warning also applies to security updates.

In limited situations, you might choose not to install a new kernel for a security update. For example, if there's a security issue related to Bluetooth hardware, it's important if there are Bluetooth components installed on your system. If there aren't, you might choose to avoid installing that update. Be aware that a security issue that affects one system could easily affect a related system as network hardware.

The kernel as built for specific distributions such as Red Hat and Ubuntu includes a number of features that differ from the stock kernel. With thousands of options, the differences are too numerous to mention. While distribution-specific kernels are built from the stock Linux kernel, the security issues related to distribution-specific kernels may vary.

But as the stock kernel, you may not want to always update a distribution-specific kernel. Some updates don't relate to security issues. Other updates may include hardware that may not be installed on your systems. In all cases, it's a risk to update a Linux kernel.
