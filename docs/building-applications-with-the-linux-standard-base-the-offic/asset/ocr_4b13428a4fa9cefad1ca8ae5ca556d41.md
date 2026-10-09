The LSB trademark can only be used by LSB-certified applications; no other statement of compliance can be made. For more information, see Section 7.2.

# 2.2 SOURCE CODE STANDARDS

The standardization of a set of Application Programming Interfaces (APIs) for the purpose of recompile compatibility between systems is a source code standard.

# 2.2.1 POSIX

The Institute of Electrical and Electronics Engineers (IEEE) is the group that has developed and continues to develop the POSIX family of standards. Beginning in the mid-1980s, this group picked up on the work already done by the UNIX user organization UniForum (the 1984 /usr/Group Standard) and began to produce an operating system standard under Project 1003 (POSIX).

The best known POSIX document is IEEE Std 1003.1 (also known as POSIX 1003.1), but the term “POSIX” actually covers a set of related operating system specifications. The various subprojects instituted under 1003 are staffed by individual volunteers representing a cross-section of skills such as hardware manufacturing, OS development, software and tools development, academia, governments, and more.

The name POSIX was suggested by Richard Stallman, one of the participants. It is pronounced pahz-icks, as in positive.

As stated in the cover material for these standards, there were several principles guiding their development, the key ones being application source portability, specification of the interface without requiring a particular implementation, and reliance on historical practice.

Another goal is *consensus*. There are some features of historical (and modern) UNIX-based operating systems which are not found in POSIX, because no consensus could be reached at the time work was being done. This is the reason there is no mention of either **tar** or **cpio** in the 1003.2 specification, for example. Where there was no consensus, the feature was left out to