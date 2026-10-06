# Chapter 3 • DEPLOYING YOUR SYSTEMS

+   • You might need to improve performance of the application with more aggressive compiler optimizations.

+   • Some applications are distributed only as source code.

When building from source, it's your responsibility to figure out where to put the software and how to manage the files it contains. As you develop experience in working with these application installations, you'll devise your own systems for managing the process. But building and managing a software repository is an effective approach that many system administrators use for tracking software installations. A software repository is a directory tree where you install all of your software; it keeps everything in one place, making software files easy to find.

# The Gnu C Compiler

The most popular compiler on Unix is GCC, the Gnu C Compiler. While GCC doesn't always produce executables as optimized as those from your operating system's compiler, the compiler is free and is almost guaranteeed to successfully compile most third-party applications. You can download GCC at http://www.gnu.org/software/gcc/gcc.html.

Keep the repository separate from any other software installation locations on your systems. You don't want to mix and match your applications with critical system infrastructure. For example, /usr may not be the best place to put your new software because system software is stored in /usr/bin, man pages are in /usr/man, and critical system libraries are in /usr/lib. You should also consider something as /usr/local, because a lot of aged software installs in that location. Ultimately, you should consult file system standards for your operating system, which define the purpose of each directory on the file system and where certain types of software should be installed. You should be able to find this information in your operating system's documentation.

Make your software repository truly unique to your systems, so it won't be clobbly by system software or third-party packages. One technique for storing your repository is to create a special directory in /usr named after your organization. If your company's name is XYZ, Inc., you may want to name this directory /usr/xyz, and place your files in /usr/xyz/bin, /usr/xyz/man, /usr/xyz/lib, and wherever else you install software files.

# GNU Configure Installs Applications Where You Want

Most software allows you to specify where it is installed, and the popular GNU configure interface provided with many open-source distributions is well suited to this storage solution. The following GNU configure directive, when executed in a directory containing source code, will ensure that all files are installed using a prefix of /usr/xyz:

```
/configure --prefix=/usr/xyz
```

You can read more about GNU configure at http://www.gnu.org/software/autoconf.