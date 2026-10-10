problem, you can fix it. In other words, you are in control of the situation and not at the mercy of a commercial developer you can't control. But having the source code means you need to be able to compile it, too. Otherwise all you have is a bunch of text files that can't do much.

Although almost every piece of software in this book is available as an RPM, we step through the process of compiling it ourselves so that we can pick and choose compile time options, which is something that we can't do with RPMs. Thus, it's a good idea to become comfortable with compiling packages yourself.

In this section, we will step through the process of compiling the SSH package, a tool that allows secure connections to remote hosts (SSH is covered in Chapter 17). SSH is a typical package; you'll find that most other packages that you need to compile follow the same general pattern.

# Getting and Unpacking the Package

Software that comes in source form is generally made available as a *tarball*—that is, it is archived into a single large file and then compressed. The tools used to do this are tar and gzip; tar handles the process of combining many files into a single large file, and gzip is responsible for the compression.

> NOTE: Do not confuse gzip with WinZip. They are two different programs that use two different (but comparable) methods of compression. It should be noted, though, that WinZip does know how to handle tarballs.

Typically, a single directory is selected in which to build and store tarballs. This allows the system administrator to keep the tarball of each package in a safe place in the event he or she needs to pull something out of it later. It also lets all the administrators know which packages are installed on the system in addition to the base system. A good directory for this is *usr/local*, since software local to a site is generally installed in *usr/local*.

Most tarballs, when unpacked, create a new directory for all of its files. The SSH tarball (ssh-2.0.13.tar.gz, for example, creates the directory ssh-2.0.13. Most packages follow this standard. If you find a package that does not follow it, it is a good idea to create a subdirectory with a reasonable name and place all the unpacked source files there. This allows multiple builds to occur at the same time without the risk of the two builds conflicting.

Begin by downloading the SSH tarball. You can fetch it from the official SSH site at http://www.ssh.fi.

To unpack the SSH tarball, first move the file into the *usr/local/src* directory, like so:

```
[root@ford /root] # mv ssh-2.0.13.tar.gz /usr/local/src
```

> NOTE: This assumes that the SSH tarball is called ssh-2.0.13.tar.gz, and it was downloaded into the /root directory.