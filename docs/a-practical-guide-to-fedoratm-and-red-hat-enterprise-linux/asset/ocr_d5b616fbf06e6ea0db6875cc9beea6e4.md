# **RAM disk**

RAM that is made to look like a floppy diskette or hard disk. A RAM disk is frequently used as part of the *boot* (page 1240) process.

# **RAS**

Remote access server. In a network, a computer that provides access to remote users via analog modem or ISDN connections. RAS includes the dial-up protocols and access control (authentication). It might be a regular filerserver with remote access software or a proprietary system, such as Shiva's LANRouter. The modems might be internal or external to the device.

# **RDF**

Resource Description Framework. Being developed by W3C (the main standards body for the World Wide Web), a standard that specifies a mechanism for encoding and transferring *metadata* (page 1260). RDF does not specify what the metadata should or can be. It can integrate many kinds of applications and data, using XML as an interchange syntax. Examples of the data that can be integrated include library catalogs and worldwide directories; syndication and aggregation of news, software, and content; and collections of music and photographs. Visit www.w3.org/RDF for more information.

# **real UID**

The UID (user ID) that a user logs in with as defined in *etc/passwd*. Differentiated from *effective UID* (page 1248). See also *UID* on page 1278.

# **redirection**

The process of directing standard input for a program to come from a file rather than from the keyboard. Also, directing standard output or standard error to go to a file rather than to the screen.

# **reentrant**

Code that can have multiple simultaneous, interleaved, or nested invocations that do not interfere with one another. Noninterference is important for parallel processing, recursive programming, and interrupt handling.

It is usually easy to arrange for multiple invocations (that is, calls to a subroutine) to share one copy of the code and any readonly data. For the code to be reentrant, however, each invocation must use its own copy of any modifiable data (or synchronized access to shared data). This goal is most often achieved by using a stack and allocating local variables in a new stack frame for each invocation. Alternatively, the caller might pass in a pointer to a block of memory that that invocation can use (usually for output), or the code might allocate some memory on a heap, especially if the data must survive after the routine returns.

Reentrant code is often found in system software, such as operating systems and teleprocessing monitors. It is also a crucial component of multithreaded programs, where the term *thread-safe* is often used instead of reentrant.
:FOUCS

# **regular character**

A character that always represents itself in an ambiguous file reference or another type of regular expression. Contrast with *special character*.

# **regular expression**

A string—composed of letters, numbers, and special symbols—that defines one or more strings. See Appendix A.

# **relative pathname**

A pathname that starts from the working directory. Contrast with *absolute pathname* (page 1236).

# **remote access server**

See *RAS*.