```
```
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
        if ((connect (outsocket, (struct sockaddr *) &socks_sa, sizeof (struct
        sockaddr_in))) == -1)
        {
            perror ("connect");
            exit (1);
        }

        snprintf (buffer, 8192, "\\ x04\\ x01%c%c%c%c%c%c", (destport >> 8) &
        0xFF, destport & 0xFF, /* <-- port */
                (char) dest_he->h_addr[0], (char) dest_he-
```
```