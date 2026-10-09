flowing into sort, and the other pipe handles data flowing back. Here is a rewrite of fsort0 that works correctly:

```
```c
void fsort(void)
{
int pfdout[2], pfdin[2], fd;
ssize_t nread;
pid_t pid;
char buf[512];

ec_negl( pipe(pfdout) )
ec_negl( pipe(pfdin) )
ec_negl( pid = fork() )
if (pid == 0) { /* child */
ec_negl( dup2(pfdout[0], STDIN_FILENO) )
ec_negl( close(pfdout[0]) )
ec_negl( close(pfdout[1]) )
ec_negl( dup2(pfdin[1], STDOUT_FILENO) )
ec_negl( close(pfdin[0]) )
ec_negl( close(pfdin[1]) )
execlp("sort", "sort", (char *)NULL);
EC_FAIL
}
/* parent */
ec_negl( close(pfdout[0]) )
ec_negl( close(pfdin[1]) )
ec_negl( fd = open("datafile", O_RDONLY) )
while (true) {
ec_negl( nread = read(fd, buf, sizeof(buf)) )
if (nread == 0)
break;
ec_negl( write(pfdout[1], buf, nread) )
}
ec_negl( close(fd) )
ec_negl( close(pfdout[1]) )
while (true) {
ec_negl( nread = read(pfdin[0], buf, sizeof(buf)) )
if (nread == 0)
break;
ec_negl( write(STDOUT_FILENO, buf, nread) )
}
ec_negl( close(pfdin[0]) )
ec_negl( waitpid(pid, NULL, 0) )
return;

EC_CLEANUP_BGN
EC_FLUSH("fsort");
EC_CLEANUP_END
}
```
```