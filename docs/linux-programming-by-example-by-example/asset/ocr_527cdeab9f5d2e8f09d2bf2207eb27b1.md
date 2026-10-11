```
int main(int argc, char *argv[])
{
int fd;
char *src;
struct stat statbuf;

/* Open the source file */
if (argc != 2) {
puts("USAGE: mmcat (file)");
exit(EXIT_FAILURE);
}
if ((fd = open(argv[1], 0_RDONLY)) < 0)
err_quit("open");

/* Get the file length for mmap */
fstat(fd, &statbuf);

/* map the input file */
if ((src = mmap(0, statbuf.st_size, PROT_READ,
MAP_SHARED, fd, 0)) < 0)
err_quit("mmap");

/* write it out */

write(STDOUT_FILENO, src, statbuf.st_size);

/* clean up */
close(fd);
munmap(src, statbuf .st_size);

exit(0);
}

void err_quit(char *msg)
{
perror(msg);
exit(EXIT_FAILURE);
}
```