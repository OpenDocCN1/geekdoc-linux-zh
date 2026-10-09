read it to get its input and write it to send back the sorted output. The parent has file descriptors that access the pipe too. It will write the unsorted data to the pipe and read the sorted data from the pipe. Here's a program that reads data from the datafile and invokes sort to sort it; the sorted data is printed:

```
void fsort0(void)   /* wrong */
{
   int pfd[2], fd;
   size_t nread;
   pid_t pid;
   char buf[512];

   ec_negl( pipe(pfd) )
   ec_negl( pid = fork() )
   if (pid == 0) {  /* child */
      ec_negl( dup2(pfd[0], STDIN_FILENO) )
      ec_negl( close(pfd[0]) )
      ec_negl( dup2(pfd[1], STDOUT_FILENO) )
      ec_negl( close(pfd[1]) )
      exec1p("sort", "sort", (char *)NULL);
      EC_FAIL
   }
   /* parent */
   ec_negl( fd = open("datafile", O_RDONLY) )
   while (true) {
      ec_negl( nread = read(fd, buf, sizeof(buf)) )
      if (nread == 0)
         break;
      ec_negl( write(pfd[1], buf, nread) )
   }
   ec_negl( close(fd) )
   ec_negl( close(pfd[1]) )
   while (true) {
      ec_negl( nread = read(pfd[0], buf, sizeof(buf)) )
      if (nread == 0)
         break;
      ec_negl( write(STDOUT_FILENO, buf, nread) )
   }
   ec_negl( close(pfd[0]) )
   ec_negl( waitpid(pid, NULL, 0) )
   return;

   EC_CLEANUP_BGN
      EC_FLUSH("fsort0");
   EC_CLEANUP_END
}
```