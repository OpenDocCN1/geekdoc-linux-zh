
# `wingatebounce.c`

```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>
#include <stdlib.h>
#include <unistd.h>

#define BUFSIZE 512
#define SOCKSPORT 1080

const char portclosed[] = "socks: Port closed/Permission denied/Something went wrong\n";

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
        printf ("Usage: %s locallistenport sockshost desthost destport\n", argv[0]);
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
    {
        perror ("bind");
        exit (1);
    }
    if ((listen (listensocket, 1)) == -1)
    {
        perror ("listen");
        exit (1);
    }

    /* background stuff */
    switch (fork ())
    {
        case -1:
            perror ("fork");
            exit (1);
            break;
        case 0:
#ifndef MYDEBUG
            close (STDIN_FILENO);
            close (STDOUT_FILENO);
            close (STDERR_FILENO);
#endif
            if (setsid () == -1)
            {
                perror ("setsid");
                exit (1);
            }
            break;
        default:
            return 0;
    }

    insocket = accept (listensocket, NULL, 0);
    if (insocket == -1)
    {
        perror ("accept");
        exit (1);
    }
    close (listensocket);
    outsocket = socket (AF_INET, SOCK_STREAM, IPPROTO_TCP);
    if ((connect (outsocket, (struct sockaddr *) &socks_sa, sizeof (struct sockaddr_in))) == -1)
    {
        perror ("connect");
        exit (1);
    }

    snprintf (buffer, 8192, "\x04\x01%c%c%c%c%c%c", (destport >> 8) & 0xFF, destport & 0xFF, /* <-- port */
              (char) dest_he->h_addr[0], (char) dest_he->h_addr[1], (char) dest_he->h_addr[2], (char) dest_he->h_addr[3]); /* <-- ip */

#ifdef MYDEBUG
    for (length = 0; length < 8; length++)
        printf ("%02X:", (unsigned char) buffer[length]);
    printf ("\n");
    for (length = 0; length < 8; length++)
        if (buffer[length] > 'A' && buffer[length] < 'z')
            printf (" %c:", (unsigned char) buffer[length]);
        else
            printf (" *:");
    printf ("\n");
#endif

    /* error checking sucks */
    send (outsocket, buffer, 9, 0);
    recv (outsocket, buffer, 8, 0);

    /* handle errors etc */
    if (buffer[1] == 0x5B)
        send (insocket, portclosed, sizeof (portclosed), 0);

#ifdef MYDEBUG
    for (length = 0; length < 8; length++)
        printf ("%02X:", (unsigned char) buffer[length]);
    printf ("\n");
    for (length = 0; length < 8; length++)
        if (buffer[length] > 'A' && buffer[length] < 'z')
            printf (" %c:", (unsigned char) buffer[length]);
        else
            printf (" *:");
    printf ("\n");
#endif

    maxfd = insocket > outsocket ? insocket : outsocket;
    while (1)
    {
        FD_ZERO (&rfds);
        FD_SET (insocket, &rfds);
        FD_SET (outsocket, &rfds);
        select (maxfd + 1, &rfds, NULL, NULL);
        if (FD_ISSET (insocket, &rfds))
        {
            length = recv (insocket, buffer, sizeof (buffer), 0);
            if (length == -1 || length == 0)
                break;
            if ((send (outsocket, buffer, length, 0)) == -1)
                break;
        }
        if (FD_ISSET (outsocket, &rfds))
        {
            length = recv (outsocket, buffer, sizeof (buffer), 0);
            if (length == -1 || length == 0)
```
