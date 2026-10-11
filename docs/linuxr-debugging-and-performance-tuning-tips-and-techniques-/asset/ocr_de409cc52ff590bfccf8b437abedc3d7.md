```
327 struct ibuf *
328 \t \t \t \t \t \t \t \t \t \t \t struct ibuf* gstat(char *file, int argf)
329 \t \t \t \t \t \t \t \t \t \t \t gstat(file, argf)
330 \t \t \t \t \t \t \t \t \t \t \t char *file;
331 \t \t \t \t \t \t \t \t \t \t \t {
332 \t \t \t \t \t \t \t \t \t \t \t \textern char \*malloc();
333 \t \t \t \t \t \t \t \t \t \t \t struct stat stath;
334 \t \t \t \t \t \t \t \t \t \t \t register struct ibuf \*rep;
335 \t \t \t \t \t \t \t \t \t \t \t static int nomomcore;
336
337 \t \t \t \t \t \t \t \t \t \t \t if (nomomcore)                Ran out of memory earlier
338 \t \t \t \t \t \t \t \t \t \t \t \treturn(NULL);
339 \t \t \t \t \t \t \t \t \t \t \t rep = (struct ibuf \*)malloc(sizeof(struct ibuf));
340 \t \t \t \t \t \t \t \t \t \t \t if (rep==NULL) {
341 \t \t \t \t \t \t \t \t \t \t \t \tfprintf(stderr, \"ls: out of memory\n\");
342 \t \t \t \t \t \t \t \t \t \t \t \tnomcore = 1;
343 \t \t \t \t \t \t \t \t \t \t \t \treturn(NULL);
344 \t \t \t \t \t \t \t \t \t \t \t }
345 \t \t \t \t \t \t \t \t \t \t \t if (lastp >= &flist[NFILES]) {      Check whether too many files given
346 \t \t \t \t \t \t \t \t \t \t \t \tstatic int msg;
347 \t \t \t \t \t \t \t \t \t \t \t \tlastp--;
348 \t \t \t \t \t \t \t \t \t \t \t \tif (msg==0) {
349 \t \t \t \t \t \t \t \t \t \t \t \t \tfprintf(stderr, \"ls: too many files\n\");
350 \t \t \t \t \t \t \t \t \t \t \t \t \tmsg++;
351 \t \t \t \t \t \t \t \t \t \t \t \t}
352 \t \t \t \t \t \t \t \t \t \t \t }
353 \t \t \t \t \t \t \t \t \t \t \t \t*lastp++ = rep;                   Fill in information
354 \t \t \t \t \t \t \t \t \t \t \t \trep->flags = 0;
355 \t \t \t \t \t \t \t \t \t \t \t \trep->inum = 0;
356 \t \t \t \t \t \t \t \t \t \t \t \trep->ltype = '-';                Default file type

```

The static variable nomcore [sic] indicates that malloc() failed upon an earlier call. Since it's static, it's automatically initialized to 0 (that is, false). If it's true upon entry, gstat() just returns NULL. Otherwise, if malloc() fails, 1s prints an error message, sets nomcore to true, and returns NULL (lines 334–343).

Lines 344–351 make sure that there is still room left in the flist array. If not, 1s prints a message (but only once; note the use of the static variable msg), and then reuses the last slot in flist.

Line 352 makes the slot lastp points to point to the new struct ibuf (rep). This also updates lastp, which is used for sorting in main() (lines 142 and 152). Lines 353–355 set default values for the flags, inode number, and type fields in the struct ibuf.