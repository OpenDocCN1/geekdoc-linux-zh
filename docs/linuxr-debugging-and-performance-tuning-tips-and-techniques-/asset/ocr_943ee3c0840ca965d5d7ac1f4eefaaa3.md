(`ftp://ftp.gnu.org/gnu/make/make-3.80.tar.gz`). It can be found in the file read.c.

Following the “no arbitrary limits” principle, lines in a Makefile can be of any length. Thus, this routine’s primary job is to read lines of any length and make sure that they fit into the buffer being used.

A secondary job is to deal with continuation lines. As in C, lines that end with a backslash logically continue to the next line. The strategy used is to maintain a buffer. As many lines as will fit in the buffer are kept there, with pointers keeping track of the start of the buffer, the current line, and the next line. Here is the structure:

```
```
struct ebuffer
{
    char *buffer;    /* Start of the current line in the buffer.  */
    char *bufnext;   /* Start of the next line in the buffer.  */
    char *bufstart;  /* Start of the entire buffer.  */
    unsigned int size;  /* Malloc’ed size of buffer.  */
    FILE *fp;      /* File, or NULL if this is an internal buffer.  */
    struct floc floc;  /* Info on the file in fp (if any) .  */
};```

```

The *size* field tracks the size of the entire buffer, and *fp* is the *FILE* pointer for the input file. The *floc* structure isn’t of interest for studying the routine.

The function returns the number of lines in the buffer. (The line numbers here are relative to the start of the function, not the source file.)

```
```
1 static long
2 readline (ebuf)                         static long readline(struct ebuffer *ebuf)
3      struct ebuffer *ebuf;
4 {
5   char *p;
6   char *end;
7   char *start;
8   long nlines = 0;
9
10  /* The behaviors between string and stream buffers are different enough to
11     warrant different functions.  Do the Right Thing.  */
12
13  if (!ebuf->fp)
14    return readstring (ebuf);
15
16  /* When reading from a file, we always start over at the beginning of the
17     buffer for each new line.  */
18
19 p = start = ebuf->bufstart;
20 end = p + ebuf->size;
21 *p = '\0';```

```