```
28 struct stat *stb;                
29 {                     
30     char *val;                
31     static size_t env_val = 0; 
32     static short first = TRUE; 
33     static short exact = FALSE;
34 
35     /* force all members to zero in case OS doesn't use all of them. */
36     memset(stb, '\0', sizeof(struct stat));
37 
38     /* always stat, in case stb is used by higher level code. */
39     if (fstat(fd, stb) == -1)
40         fatal("can't stat fd %d (%s)", fd, strerror(errno));
41 
42     if (first) {
43         first = FALSE;
44 
45         if ((val = getenv("AWKBUFSIZE")) != NULL) {
46             if (strcmp(val, "exact") == 0)
47                 exact = TRUE;
48             else if (ISDIGIT(*val)) {
49                 for (; *val && ISDIGIT(*val); val++)
50                     env_val = (env_val * 10) + *val - '0';
51 
52                 return env_val;
53             }
54         }
55     } else if (! exact && env_val > 0)
56         return env_val;
57     /* else
58         fall through */
59 
60     /*
61      * System V,n. n < 4, doesn't have the file system block size in the
62      * stat structure.  So we have to make some sort of reasonable
63      * guess.  We use stdio's BUFSIZ, since that is what it was
64      * meant for in the first place.
65      */
66 #ifdef HAVE_ST_BLKSIZE
67 #define DEFBFLKSZ     (stb->st_blksize > 0 ? stb->st_blksize : BUFSIZ)
68 #else
69 #define DEFBFLKSZ     BUFSIZ
70 #endif
71 
72     if (S_ISREG(stb->st_mode)            /* regular file */
73         && 0 < stb->st_size              /* non-zero size */
74         && stb->st_size < DEFBFLKSZ      /* small file */
75             ||  exact) {                 /* or debugging */
76         return stb->st_size;             /* use file size */
77     }
78     return DEFBFLKSZ;
79 }
```