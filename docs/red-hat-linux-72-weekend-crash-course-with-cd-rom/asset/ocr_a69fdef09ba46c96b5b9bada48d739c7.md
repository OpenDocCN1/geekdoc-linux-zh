![](bbox=[0.09, 0.1, 0.25, 0.24])

# Building Software Packages from Source Files

# Session Checklist

+   
+   1. Downloading and unpacking software
+   2. Building and installing software from source files
+   

![](bbox=[0.0, 0.52, 0.08, 0.58])

In Session 23, you learned how to install software packages distributed in the Red Hat Package Manager (RPM) format. RPM files bundle all the executable binary files and configuration files needed to install a software package. However, many open source software packages are distributed in source code form without any executable binaries. Before you can use such software, you have to build the executable binary files and then follow some instructions to install the package. This session shows you how to download and unpack the source files. It then shows you how to build software packages from source files and install them.

# Downloading and Unpacking the Software

Open source files are typically distributed in compressed tar archives. As you learned in Session 26, the tar program creates these archives and then the gzip program compresses them. The distribution is in the form of a single large file with a .tar.gz or .tar.Z extension, which is often referred to as a compressed or gzipped tarball. If you want the software, you have to download the compressed tarball and unpack it.

You download the compressed tar file using anonymous File Transfer Protocol (FTP) or the Web browser. Typically, this action involves no more effort on your part than clicking a link and saving the file in an appropriate directory on your system.

To try your hand at downloading and building a software package, you can practice on the X Multimedia System (XMS), which is a graphical X application for playing MP3 files and other multimedia files. XMS is bundled with Red Hat Linux and installed on your system when you select the Multimedia Support package group during Red Hat Linux installation. However, there is no harm in downloading and rebuilding the XMS package again.