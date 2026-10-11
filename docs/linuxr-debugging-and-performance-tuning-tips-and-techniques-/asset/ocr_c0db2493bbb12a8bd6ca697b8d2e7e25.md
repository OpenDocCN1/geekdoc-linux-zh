Line 51 computes the number of file descriptors nftw() can use. We don't want it to use all available file descriptors in case the callback function wants to open files too. The computation uses getdtablesize() (see Section 4.4.1, “Understanding File Descriptors,” page 92) to retrieve the maximum available number and subtracts SPARE_FDS, which was defined earlier, on line 13.

This procedure warrants more explanation. In the normal case, at least three descriptors are already used for standard input, standard output, and standard error, nftw() needs some number of file descriptors for opening and reading directories; under the hood, opendir() uses open() to open a directory for reading. If the callback function also needs to open files, we have to prevent nftw() from using up all available file descriptors with open directories. We do this by subtracting some number from the maximum available. For this example, we chose five, but if the callback function needs to open files, a larger number should be used. (nftw() knows how to recover when it runs out of file descriptors; we don't have to worry about that case.)

Lines 52–58 are the main loop over the arguments; lines 53–57 check for errors; when they occur, the code prints a diagnostic and increments the errors variable.

Lines 60–64 are part of the experiment for FTFW_CHDIR, printing the starting and finishing directories if -c was used.

The function of real interest is process(); this is the callback function that processes each file. It uses the basic template for an nftw() callback function, which is a switch statement on the flag value:

```
```c
69  /* process -- print out each file at the right level */
70  /*
71  int process(const char *file, const struct stat *sb,
72            int flag, struct FTW *s)
73  {
74      int retval = 0;
75      const char *name = file + s->base;
76
77      printf("%*s", s->level * 4, "");  /* indent over */
78
79      switch (flag) {
80      case FTW_F:
81          printf("%s (file)\n", name);
82          break;
83      case FTW_D:
84          printf("%s (directory)\n", name);
85          break;
```
```