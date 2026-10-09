```
strcpy(p->pt_name_s, s);
#if defined(MASTER_NAME_SEARCH)
strcpy(p->pt_name_s, p->pt_name_m);
p->pt_name_s[PTY_MS] = 't';
#else
errno = ENOSYS;
EC_FAIL
#endif
return p;

EC_CLEANUP_BGN
if (p != NULL) {
(void)close(p->pt_fd_m);
(void)close(p->pt_fd_s);
free(p);
}
return NULL;
EC_CLEANUP_END
```

Step 4, forking to create a child process, is done by the program that uses the library—there's no library function to do it.

Step 5 is to call setsid (Section 4.3.2) in the child to make it relinquish its controlling terminal because we want the pty to be the controlling terminal. Step 6, also done in the child, is to open the slave side, whose name we already have. Those two steps are done by pt_open_slave:

```
bool pt_open_slave(PTINFO *p)
{
ec_neg1( setsid() )
if (p->pt_fd_s != -1)
ec_neg1( close(p->pt_fd_s) )
ec_neg1( p->pt_fd_s = open(p->pt_name_s, O_RDWR) )
#if defined(NEED_TIOCSTTY)
ec_neg1( ioctl(p->pt_fd_s, TIOCSTTY, 0) )
#endif
#if defined(NEED_OSTREAM_SETUP)
ec_neg1( ioctl(p->pt_fd_s, I_PUSH, "ptem" )
ec_neg1( ioctl(p->pt_fd_s, I_PUSH, "ldterm" ) )
#endif
/*
Changing mode not that important, so don't fail if it doesn't
work only because we're not superuser.
*/
if (fchmod(p->pt_fd_s, PERM_FILE) == -1 && errno != EPERM)
EC_FAIL
return true;
```