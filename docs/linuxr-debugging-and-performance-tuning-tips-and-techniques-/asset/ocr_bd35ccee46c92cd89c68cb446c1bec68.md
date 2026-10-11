```
```c
20 int main(int arge, char *argv)
21 {
22     int c;
23     char *file = "/etc/mtab";  /* default file to read */
24
25     myname = argv[0];
26     while ((c = getopt(arge, argv, "f:") != -1) {
27         switch (c) {
28             case 'f':
29                 file = optarg;
30                 break;
31             default:
32                 fprintf(stderr, "usage: %s [-f fstab-file]\n", argv[0]);
33                 exit(1);
34         }
35     }
36
37     process(file);
38     return (errors != 0);
39 }
40
41 /* process --- read struct mntent structures from file */
42
43 void process(const char *filename)
44 {
45     FILE *fp;
46     struct mntent *fs;
47
48     fp = setmntent(filename, "r");  /* read only */
49     if (fp == NULL) {
50         fprintf(stderr, "%s: %s: could not open: %s\n",
51                 myname, filename, strerror(errno));
52         exit(1);
53     }
54
55     while ((fs = getmntent(fp)) != NULL)
56         do_statvfs(fs);
57
58     endmntent(fp);
59 } ```
```

Lines 1-59 are essentially the same as ch08-mounted.c.main() handles the command line, and process() loops over each mounted filesystem. do_statvfs() does the real work, printing the struct statvfs for each interesting filesystem.