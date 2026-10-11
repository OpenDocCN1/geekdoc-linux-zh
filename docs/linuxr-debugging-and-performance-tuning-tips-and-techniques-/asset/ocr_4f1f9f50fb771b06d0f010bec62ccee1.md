A final point worth noting is that in C, character constants (such as `'x'`) have type `int`, not `char`. $ ^{1} $ So there’s no problem putting such constants into an integer array; everything works correctly.

```
277 char *             char *makename(char *dir, char *file)
278 makename(dir, file)
279 char *dir, *file;
280 {
281     static char dfile[100];
282     register char *dp, *fp;
283     register int i;
284
285     dp = dfile;
286     fp = dir;
287     while (*fp)
288         *dp++ = *fp++;
289     *dp++ = '/';
290     fp = file;
291     for (i=0; i<DIRSIZ; i++)
292         *dp++ = *fp++;
293     *dp = 0;
294     return(dfile);
295 }
```

Lines $277-295$ define the `makename()` function. Its job is to concatenate a directory name and a filename, separated by a slash character, and produce a string. It does this in the `static buffer dfile`. Note that `dfile` is only 100 characters long and that no error checking is done.

The code itself is straightforward, copying characters one at a time. `makename()` is used by the `readdir()` function.

```
297 readdir(dir)             void readdir(char *dir)
298 char *dir;
299 {
300     static struct direct dentry;
301     register int j;
302     register struct iobuf *ep;
303
304     if ((dirf = fopen(dir, "r")) == NULL) {
305         printf("%s unreadable\n", dir);
306         return;
307     }
308     tblocks = 0;
```