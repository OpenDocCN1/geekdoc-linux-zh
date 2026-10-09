By default, the read system call also acts on terminals differently from the way it acts on files: It never returns more than one line of input, and no characters are returned until the entire line is ready, even if the read requests only a single character. This is because until the user has ended the line, we can’t assume it’s in final form—the erase and kill characters can be used to revise it or to cancel it entirely. The count returned by read is used to determine how many characters were actually read. (What we just described is called canonical terminal input, but you can disable it; see Section 4.5.9.)

The user can end a line in one of two ways. Most often, a newline character is the terminator. The return key is pressed, but the device driver translates the return (octal 15) to a newline (octal 12). Alternatively, the user can generate an end-of-file (EOF) character by pressing Ctrl-d. In this case the line is made available to read as is, without a newline terminator. One special case is important: If the user generates an EOF at the start of the line, read will return with a zero count, since the line that the EOF terminated is empty. This looks like an end-of-file, and that’s why Ctrl-d can be thought of as an end-of-file “character.”

The following function can be used to read a terminal using the standard-input file descriptor STDIN_FILENO (defined as 0). It removes a terminating newline character if one is present, and adds a terminating null character to make the line into a C string.

```
```c
bool getln(char *s, size_t max, bool *iseof)
{
    size_t nread;

    switch (nread = read(STDIN_FILENO, s, max - 1)) {
    case -1:
        EC_FAIL
    case 0:
        *iseof = true;
        return true;
    default:
        if (s[nread - 1] == '\n')
            nread--;
        s[nread] = '\0';
        *iseof = false;
        return true;
    }

    EC_CLEANUP_BGN
    return false;
    EC_CLEANUP_END
}
```
```