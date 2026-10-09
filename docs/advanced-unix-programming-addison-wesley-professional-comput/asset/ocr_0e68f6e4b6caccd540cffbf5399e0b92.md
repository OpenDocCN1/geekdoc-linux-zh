The return value is used to indicate an error, so an EOF is indicated with the third argument, as in this calling example:

```
ec_false( getline (s, sizeof(s), &iseof) )
if (iseof)
    printf ("EOF\n" );
else
    printf ("Read: %s\n", s);
```

getline is efficient for terminals because it reads the entire line with a single system call. Furthermore, it doesn't have to search for the end- it just goes by the count returned by read. But it doesn't work on files or pipes at all because, since the one-line limit doesn't apply, read will in general read too much. Instead of getline reading a line, it will read the next max - 1 characters (assuming that many characters are present).

A more universal version of getline would ignore that unique property of terminals - reading one line at most. It would simply examine each character, looking for a newline:

```
bool getline2 (char *s, ssize_t max, bool *iseof)
{
    ssize_t n;
    char c;

    n = 0;
    while (true)
        switch (read (STDIN_FILENO, &c, 1)) {
        case -1:
            EC_FAIL
        case 0:
            s[n] = `\0`;
            *iseof = true;
            return true;
        default:
            if (c == `\n`) {
                s[n] = `\0`;
                *iseof = false;
                return true;
            }
            if (n >= max - 1) {
                errno = E2BIG;
                EC_FAIL
            }
            s[n++] = c;
        }
}
```