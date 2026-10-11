```
35 unsigned long myrandom(void)
36 {
37 static int fd = -1;
38 unsigned long data;
39
40 if (fd == -1)
41 fd = open("/dev/urandom", O_RDONLY);
42
43 if (fd == -1 || read(fd, &data, sizeof(data)) <= 0)
44 return random(); /* fall back */
45
46 return data;
47 }
48
49 /* main --- print N different die faces */
50 int main(int argc, char **argv)
51 {
52 int nfaces;
53 int i, j, k;
54
55 ... check args, compute nfaces, as before ...
56
68
69 for (i = 1; i <= nfaces; i++) {
70 j = myrandom() % 6; /* force to range 0 <= j <= 5 */
71 printf("%*s\n", j);
72 for (k = 0; k < 3; k++)
73 printf("| |%s|\n", die_faces[j * 3] + k)];
74 printf("+-------+\n");
75 putchar('\n');
76 }
77
78 return 0;
79 }
```

Lines 35–47 provide a function-call interface to /dev/urandom, reading an unsigned long’s worth of data each time. The cost is one file descriptor that remains open throughout the program’s life.

# 12.7 Metacharacter Expansions

Three sets of functions, of increasing complexity, provide the ability to match shell wildcard patterns. Many programs need such library functions. One example is find: ‘find . -name ‘*.c’ -print’. Another is the -exclude option in many programs that accepts a wildcard pattern of files to exclude from some action or other. This section looks at each set of functions in turn.