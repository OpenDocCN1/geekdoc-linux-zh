nm lists the symbols stored in file, which must be a static library or archive file, as described in the preceding section. options controls nm's behavior. Table 29-3 describes useful options for nm.

| Option | Description |
| --- | --- |
| -C | Converts symbols names into user-level names. This is especially useful for making C++ function names readable. |
| -l | Uses debugging information to print the line number where each symbol is defined, or the relation if the symbol is undefined. |
| -s | When used on archive (.a) files, prints the index that maps symbol names to the modules or members in which the symbol is defined. |
| -u | Displays only undefined symbols, symbols defined externally to the file being examined. |

Here's an example using nm to show the symbols of in /usr/lib/libld.a:

$ /usr/lib/libld.a | head

```
dlopen.o:
00000040 T _dlopen_check
U _dl_open
U _dlerror_run
00000040 W dlopen
00000040 t dlopen_doit

dlclose.o:
U _dl_close
```

# The ar Command

ar creates, modifies, extracts archives. It is most commonly used to create static libraries, which are files that contain one or more object files. ar also creates and maintains a table that cross-references symbol names to the members in which they are defined. The ar command has the following syntax:

```
ar (dmprtqx) [options] [member] archive file [...]
```

ar creates the archive named archive from the file(s) listed in file. At least one of d, m, p, q, r, t, and x is required. You usually use r. Table 29-4 lists the most commonly used options.