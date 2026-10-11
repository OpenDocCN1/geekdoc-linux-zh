*size_t* size  The number of bytes to allocate.

memalign() is a nonstandard but widely available function that works similarly. The return value is NULL on failure or the requested storage on success, with *boundary* (a power of 2) indicating the alignment and *size* indicating the requested amount of memory.

Traditionally, storage allocated with memalign() could *not* be released with free(), since memalign() would allocate storage with malloc() and return a pointer to a suitably-aligned byte somewhere within that storage. The GLIBC version does not have this problem. Of the two, you should use posix_memalign() if you have it.

# 14.2 Locking Files

Modern Unix systems, including GNU/Linux, allow you to lock part or all of a file for reading and writing. Like many parts of the Unix API that developed after V7, there are multiple, conflicting ways to do file locking. This section covers the possibilities.

# 14.2.1 File Locking Concepts

Just as the lock in your front door prevents unwanted entry into your home, a *lock* on a file prevents access to data within the file. File locking was added to Unix after the development of V7 (from which all modern Unix systems are descended) and thus, for a while, multiple, conflicting file-locking mechanisms were available and in use on different Unix systems. Both BSD Unix and System V had their own incompatible locking calls. Eventually, POSIX formalized the System V way of doing file locks. Fortunately, the names of the calls were different between System V and BSD, so GNU/Linux, in an effort to please everyone, supports both kinds of locks.

Table 14.1 summarizes the different kinds of locks.

There are multiple aspects to locking, as follows:

# Record locking

A record lock is a lock on a portion of the file. Since Unix files are just byte streams, it would be more correct to use the term *range lock* since the lock is on a range of bytes. Nevertheless, the term “record lock” is in common use.