```
```c
int
main (int argc, char **argv)
{
int listensocket, insocket, outsocket;
short listenport, destport;
struct hostent *socks_he, *dest_he;
struct sockaddr_in listen_sa, socks_sa;
int sopts = 1, maxfd;
char buffer[BUFSIZE];
int length;
fd_set rfds;

if (argc != 5)
{
printf ("Usage: %s locallistenport sockshost desthost destpor
 t\n", argv[0]);
exit (1);
}

if ((socks_he = gethostbyname (argv[2])) == NULL)
{
herror ("gethostbyname");
exit (1);
}

memset (&socks_sa, 0, sizeof (struct sockaddr_in));
memcpy (&socks_sa.sin_addr.s_addr, socks_he->h_addr_list[0], socks_he->h_length);
if ((dest_he = gethostbyname (argv[3])) == NULL)
{
herror ("gethostbyname");
exit (1);
}

/* no need for errorchecking. only fools mess these up */
listenport = atoi (argv[1]);
destport = atoi (argv[4]);

listensocket = socket (AF_INET, SOCK_STREAM, IPPROTO_TCP);
setsockopt (listensocket, SOL_SOCKET, SO_REUSEADDR, &sopts, sizeof (int));

memset (&listen_sa, 0, sizeof (struct sockaddr_in));

listen_sa.sin_port = htons (listenport);
listen_sa.sin_addr.s_addr = htonl (INADDR_ANY);

socks_sa.sin_port = htons (SOCKSPORT);

if (bind (listensocket, (struct sockaddr *) &listen_sa, sizeof (struct sockaddr_in)) == -1)
```
```