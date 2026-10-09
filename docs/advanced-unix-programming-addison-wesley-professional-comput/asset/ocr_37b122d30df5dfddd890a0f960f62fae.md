+   100% implementation of 290 or so interfaces out of the 1108 that are in the SUS. Excluded are Standard C functions, POSIX threads, user-level functions such as bsearch and accounting, spawning, tracing, obsoleted functions, and a few others.

+   All errors thrown, never returned. Thrown object is a type that includes errno and other error codes (e.g., from getaddrinfo).

+   No memory dynamically allocated unless the word “alloc” appears in the member-function name, and very few instances of that.

+   Space and time efficiency very close to native C SUS, except for member-function-call overhead.

+   Objects reflect organization of UNIX and SUS objects (e.g., File, Dir, DirStream, Process). That is, Ux implements UNIX abstractions rather than introducing different ones.

+   Where re-entrant and non-re-entrant functions are defined (e.g., readdir and readdir_r), usually the re-entrant version is used and the buffer is in the object. If necessary, an “alloc” member function is provided to allocate storage for it (see #4, above).

+   No additional error checking over what the SUS function provides. For example, if a NULL pointer is passed to File::open, it is passed directly to the underlying open.

+   Automatically chooses, for example, fchown over chown if the object is open. Single member function File::chown for both.

+   Automatically detects whether an error occurred in some cases. For example, for pathconf, a -1 return is an error only if errno changed.

+   Some functions coalesced with use of optional arguments. For example, read/pread, write/pwrite, fsync/fdatasync.

+   No copy constructors or assignment operators other than default. Follows from #4, in part.

Here's the Ux class hierarchy:

```
Ux::Base
    Ux::Aio
    Ux::Clock
    Ux::DirStream
```