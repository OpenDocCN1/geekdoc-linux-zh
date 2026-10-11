have been processed.$^9$ The GNU/Linux $nftw(3)$ manpage notes for FTW_PHYS that “this is what you want.” This lets you process symbolic links as themselves, which is usually what’s necessary. (Consider du; it should count the link’s space separately from that of the linked-to file.)

# 8.4.3.2 The nftw() Callback Function

As $nftw()$ runs, it calls a function to which you supply a pointer. (Such functions are termed *callback functions* since they are “called back” from library code.) The callback function receives four arguments:

```
```
const char *file
```

    The name of the current file (directory, symbolic link, etc.) being processed.
```

```
```
const struct stat *sb
```

    A pointer to a `struct stat` for the file.
```

```
```
int flag
```

    One of several flag values (described below) indicating what kind of file this is or whether an error was encountered for the object.
```

```
```
struct FTW *s
```

    This structure provides two separate pieces of information:
```

```
```
struct FTW {
    int base;      /* Index in file of base part of filename */
    int level;     /* Depth of this item relative to starting point */
};
```

```

The $flag$ parameter has one of the values listed in Table 8.4.

The `struct FTW *s` provides additional information that can be useful. `s->base` acts as an index into `file`; `file` is the full pathname of the object being processed (relative to the starting point). ‘`file` + `s->base`’ points to the first character of the filename component of the file.