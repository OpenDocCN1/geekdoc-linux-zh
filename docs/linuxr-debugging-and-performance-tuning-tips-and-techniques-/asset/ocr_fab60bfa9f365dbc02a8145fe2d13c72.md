can be purchased from ANSI ${ }^{2}$ and from ISO. ${ }^{3}$ (The PDF version of the C standard is quite affordable.)

The POSIX standard can be ordered from The Open Group. ${ }^{4}$ By working through their publications catalog to the items listed under “CAE Specifications,” you can find individual pages for each part of the standard (named “C031” through “C034”). Each one’s page provides free access to the online HTML version of the particular volume.

The POSIX standard is intended for implementation on both Unix and Unix-like systems, as well as non-Unix systems. Thus, the base functionality it provides is a subset of what Unix systems have. However, the POSIX standard also defines optional exten- sions—additional functionality, for example, for threads or real-time support. Of most importance to us is the X/Open System Interface (XSI) extension, which describes facilities from historical Unix systems.

Throughout the book, we mark each API as to its availability: ISO C, POSIX, XSI, GLIBC only, or nonstandard but commonly available.

# Features and Power: GNU Programs

Restricting ourselves to just the original Unix code would have made an interesting history book, but it would not have been very useful in the 21st century. Modern programs do not have the same constraints (memory, CPU power, disk space, and speed) that the early Unix systems did. Furthermore, they need to operate in a multilingual world-ASCII and American English aren’t enough.

More importantly, one of the primary freedoms expressly promoted by the Free Software Foundation and the GNU Project ${ }^{5}$ is the “freedom to study.” GNU programs are intended to provide a large corpus of well-written programs that journeyman pro- grammers can use as a source from which to learn.

+   * http://www.ansi.org
+   
+   * http://www.iso.ch
+   
+   * http://www.opengroup.org
+   
+   * http://www.gnu.org