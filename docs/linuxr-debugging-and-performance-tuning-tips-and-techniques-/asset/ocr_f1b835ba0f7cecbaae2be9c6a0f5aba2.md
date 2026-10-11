```
39 struct lbuf *firstp = flist;  
40 char *dotp = ".";  
41  
42 char *makename();  
43 struct lbuf *gstat();  
44 char *ctime();  
45 long nblock();  
46  
47 #define ISARG 0100000
```

The program starts with file inclusions (lines 5–8) and variable declarations. The struct lbuf (lines 14–27) encapsulates the parts of the struct stat that are of interest to ls. We see later how this structure is filled.

The variables aflg, dflg, and so on (lines 29 and 30) all indicate the presence of the corresponding option. This variable naming style is typical of V7 code. The flist, lastp, and firstp variables (lines 37–39) represent the files that ls reports information about. Note that flist is a fixed-size array, allowing no more than 1024 files to be processed. We see shortly how all these variables are used.

After the variable declarations come function declarations (lines 42–45), and then the definition of ISARG, which distinguishes a file named on the command line from a file found when a directory is read.

```
49 main(argc, argv)  
50 char *argv[];  
51 {  
52 int i;  
53 register struct lbuf *ep, **ep1;  
54 register struct lbuf **slastp;  
55 struct lbuf *nbp;  
56 struct lbuf lb;  
57 char *t;  
58 int compar();  
59  
60 setbuf(stdout, stdbuf);  
61 time(&lb.lmtime);  
62 year = lb.lmtime - 6L*30L*24L*60L*60L; /* 6 months ago */
```

The main() function starts by declaring variables and functions (lines 52–58), setting the buffer for standard output, retrieving the time of day (lines 60–61), and computing the seconds-since-the-Epoch value for approximately six months ago (line 62). Note that all the constants have the L suffix, indicating the use of long arithmetic.

```
63 if (--argc > 0 && *argv[1] == '-') {  
64 argv++;  
65 while (*++*argv) switch (**argv) {
```