system using the tiny socket library. It should be invoked with:
getfile <machine_name> <remote_file_name> <local_file_name>

```
**************************************************************/
main(int argc, char **argv)
{
    SOCKET *sp;
    FILE *fp;
    int sd, i;
    char namlen, c;

    /* Check correct usage */
    if (argc!=4)
        fatal("command line parameters");

    /* Open local file */
    if ((fp = fopen(argv[3], "w"))==0)
        fatal("opening local file");

    /* Create client's socket */
    if ((sp = sopen())==0)
        fatal("sopen()");

    /* Make contact with server */
    if ((sd = sclient(sp, argv[1], PORT))==-1)
        fatal("sclient()");

    /* Get length of remote file name */
    namlen = strlen(argv[2]);

    /* Send name length to server */
    if (write(sd, &namlen, 1)!=1)
        fatal("sending namlen");

    /* Send name to server */
    for (i = 0; i<namlen; ++i)
        if (write(sd, &argv[2][i], 1)!=1)
            fatal("sending file name");

    /* Read file bytes from server */
    while ((i = read(sd, &c, 1))!=0)
        if (i==-1)
            fatal("reading remote file");
        /* Write bytes to local file */
        else if (putc(c, fp)==EOF)
            fatal("writing local file");
}
```