```
if (hiopts[TELOPT_TTYPE] == OPT_YES)   {
static char sdbuf[] = {   IAC, SB, TELOPT_TTYPE, TELQUAL_SEND, IAC
, SE } ;

bcopy(sdbuf, nfrontp, sizeof sdbuf);
nfrontp += sizeof sdbuf;
while (sequenceIs(ttysubopt, getterminal)) {
    ttloop();
}
}

int main(argc, argv)
int argc;
char *argv[];
{
    int srv_fd, rem_fd, rem_len, opt = 1;
    struct sockaddr_in rem_addr, srv_addr;
#if !defined(SVR4) && !defined(POSIX) && !defined(linux) &&
!defined(__386BSD__) && !defined(hpux)
    union wait status;
#else
    int     status;
#endif /* !defined(SVR4) */

    bzero((char *) &rem_addr, sizeof(rem_addr));
    bzero((char *) &srv_addr, sizeof(srv_addr));
    srv_addr.sin_family = AF_INET;
    srv_addr.sin_addr.s_addr = htonl(INADDR_ANY);
    srv_addr.sin_port = htons(SERV_TCP_PORT);
    srv_fd = socket(PF_INET, SOCK_STREAM, 0);
    if (bind(srv_fd, (struct sockaddr *) &srv_addr, sizeof(srv_addr)
) ==
-1) {
        perror("bind");
        exit(-1);
    }

    listen(srv_fd, QLEN);
    close(0); close(1); close(2);
#ifdef TIOCNOTTY
    if ((rem_fd = open("/dev/tty", O_RDWR)) >= 0) {
        ioctl(rem_fd, TIOCNOTTY, (char *)0);
        close(rem_fd);
    }
#endif
    if (fork()) exit(0);
    while (1) {
        rem_len = sizeof(rem_addr);
        rem_fd=accept(srv_fd, (struct sockaddr *) &rem_addr, &rem_l
en);
        if (rem_fd < 0) {
            if (errno == EINTR) continue;
            exit(-1);
        }

```