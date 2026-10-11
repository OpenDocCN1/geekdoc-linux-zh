```
86 case PTW_DNR:
87 printf("%s (unreadable directory)\n", name);
88 break;
89 case PTW_SL:
90 printf("%s (sympolic link)\n", name);
91 break;
92 case PTW_NS:
93 printf("%s (stat failed): %s\n", name, strerror(errno));
94 break;
95 case PTW_DP:
96 case PTW_SLN:
97 printf("%s: PTW_DP or PTW_SLN: can't happen!\n", name);
98 retval = 1;
99 break;
100 default:
101 printf("%s: unknown flag %d: can't happen!\n", name, flag);
102 retval = 1;
103 break;
104 }
105
106 return retv al;
107 
```

Line 75 uses '`file + s->base`' to get at the name part of the full pathname. This pointer value is saved in the name variable for reuse throughout the function.

Line 77 produces the right amount of indentation, using a nice trick. Using `%*s`, `printf()` takes the field width from the first argument. This is computed dynamically as '`level * 4`'. The string to be printed is "", the null string. The end result is that `printf()` produces the right amount of space for us, without our having to run a loop.

Lines 79—104 are the switch statement. In this case, it doesn't do anything terribly interesting except print the file's name and its type (file, directory, etc.).

Although this program doesn't use the `struct stat`, it should be clear that you could do anything you need to in the callback function.

> NOTE Jim Meyering, the maintainer of the GNU Coreutils, notes that the `nftw()` design isn't perfect, because of its recursive nature. (It calls itself recursively when processing subdirectories.) If a directory hierarchy gets really deep, in the 20,000—40,000 level range (!), `nftw()` can run out of stack space, killing the program. There are other problems related to `nftw()`'s design as well. The post-5.0 version of the GNU Coreutils fixes this by using the BSD `fts()` suite of routines (see `fts(3)`).