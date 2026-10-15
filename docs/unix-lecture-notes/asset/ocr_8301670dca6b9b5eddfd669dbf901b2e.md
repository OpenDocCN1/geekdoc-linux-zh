successively larger buffer sizes, recording the three components of running time reported by the time command for each run, and tabulating results. The revised program, called cp2.c, is in the listing below.

```
1 Listing cp2.c: a version of cp with buffer size given on the
2             command line
3 // includes and defines omitted here
4
5 int main(int argc, char *argv[])
6 {
7     int     BUFFERSIZE;
8     char    endptr[255];
9     int     source_fd, target_fd, n_chars;
10    char    *buf;
11
12    // need to check for 3 arguments instead of 2
13    if ( argc != 4 ){
14        fprintf(stderr,
15            "usage: %s_buffersize_source_destination\n",
16            argv[0]);
17        exit(1);
18    }
19
20    // extract number from string
21    BUFFERSIZE = strtol(argv[1], (char**) &endptr, 0);
22    if (BUFFERSIZE == 0) {
23        fprintf(stderr,
24            "usage:%_buffersize_must_be_a_number\n");
25        exit(1);
26    }
27
28    // SNIP: code cut out here, including error handling
29
30    /* allocate buffer of size BUFFERSIZE */
31    buf = (char*) calloc(BUFFERSIZE, sizeof(char));
32    if ( NULL == buf ) {
33        fprintf(stderr,
34            "Could_not_allocate_memory_for_buffer.\n");
35        exit(1);
36    }
37
38    // Everything else is the same from this point forward,
39    // and omitted from the listing
```

For those who have not seen it before, calloc() (in line 30) and its companion, malloc() are dynamic memory allocation functions in C. The prototype for calloc() is

```
void *calloc(size_t nelem, size_t elsize);
```