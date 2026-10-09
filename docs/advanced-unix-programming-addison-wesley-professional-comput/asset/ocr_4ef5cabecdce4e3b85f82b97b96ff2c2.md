One call instead of two is convenient, but more importantly, pread and pwrite
avoid the problem of the file offset being changed by another process or thread
between an lseek and the following read or write. Recall that this could hap-
pen, as threads could use the same file descriptor, and processes could have
duplicates that share a file offset, as explained in Section 2.2.3. This is the same
problem that O_APPEND avoids (Section 2.8). As neither pread nor pwrite even
use the file offset, they can’t get the position wrong.

To show pread in action, here’s another version of backward (from the previ-
ous section). It’s more straightforward—easier to write and debug—because the
funny business with calling lseek to decrement the file offset by -2 is gone:

```
void backward2(char *path)
{
	char s[256], c;
	int i, fd;
	off_t file_size, where;

	ec_neg1( fd = open(path, O_RDONLY) )
	ec_neg1( file_size = lseek(fd, 0, SEEK_END) )
	i = sizeof(s) - 1;
	s[i] = '\0';
	for (where = file_size - 1; where >= 0; where--)
		switch (pread(fd, &c, 1, where)) {
		case 1:
			if (c == '\n') {
				printf("%s", &s[i]);
				i = sizeof(s) - 1;
			}
			if (i <= 0) {
				errno = EZBIG;
				EC_FAIL
			}
			s[--i] = c;
			break;
		case -1:
			EC_FAIL
			break;
		default: /* impossible */
			errno = 0;
			EC_FAIL
		}
	printf("%s", &s[i]);
	ec_neg1( close(fd) )
	return;
}
```