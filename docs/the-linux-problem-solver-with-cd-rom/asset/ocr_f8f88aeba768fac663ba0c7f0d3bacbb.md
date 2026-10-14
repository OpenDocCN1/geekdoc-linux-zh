# 6

# INSTALLING SOFTWARE
FROM SOURCE CODE

# 6.1 Binary and Source Distributions

Developers traditionally distributed packages for Unix as source code. There are various reasons for this: Binaries don’t work over different architectures and operating systems, it makes local modifications to programs possible, users can install bug fixes, and so on.

Because source code is the most common way to distribute Unix packages, knowing how to install stuff from source is helpful even if you’re not a programmer. You may want to use a version that doesn’t have a binary release, configure it with different default options, or put it in a different place.

Some administrators install as many packages as possible from source—anything the systems administrator doesn’t feel is a core part of a Unix system goes elsewhere on the system, usually in the /usr/local hierarchy. The main advantage to putting files in /usr/local is that everything there survives major operating system upgrades.

Thankfully, building software is not nearly the hassle that it used to be. Most software is written in ANSI C, and widespread use of GNU autoconf has taken much of the pain out of configuration. (Of course, some packages just have to be different—deal with those as best you can.)