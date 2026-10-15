
```
/* get the key associated with the userid and put the key into snkey */
while (fgets(message, sizeof(message), in_file) != NULL)
    if (strncmp(message, "99 %", 3) == 0) {
        sscanf(message, "99 %d %d %d %d %d %d %d %d %d %d",
               &oct1, &oct2, &oct3, &oct4, &oct5, &oct6, &oct7, &oct8, &cksum);
        for (i = 0; i < 8; i++) {
            if ((strncmp(id, id, 8)))
                snkey[0] = oct1;
                snkey[1] = oct2;
                snkey[2] = oct3;
                snkey[3] = oct4;
                snkey[4] = oct5;
                snkey[5] = oct6;
                snkey[6] = oct7;
                snkey[7] = oct8;
                break;
        }
    }

    *in_id = '\0';

fclose(in_file);

/* compute the challenge/response, give them the challenge,
   and get the response from the user */
installkey(snkey, key);
bindnsck(pdy, challenge, response);
printf("%s: %s\nEnter Response: ", challenge);

if (setjmp(env) == 0) {
    alarm(SIGNTIMIT);
    fgets(reply, sizeof(reply), stdin);
    alarm(0);
    for (p = reply; isalpha(*p); isdigit(*p); p++);
        *p = '\0';
} else
    fprintf(stderr, "Timeout...\n");
    quit();

for (i=0; i<7; i++)
    if (islower(reply[i]))
        reply[i] = toupper(reply[i]);

/* if the reply the user gives doesn't match with the response we compute,
   they're out of here! */
if (strncmp(response, reply, 8) != 0) {
    syslog(LOG_NOTICE, "Failed SN login for %s from %s (%s)", id, from_host, from_ip);
    fprintf(stderr, "Incorrect response...\n");
    quit();
}
else {
    start_login(secured);
    syslog(LOG_ERR, "Can't start login process: %m");
    fprintf(stderr, "Problems starting %s... PATH LOGIN:", ...);
}
quit();
}

timeout(sig)
int sig;
{
    signal(sig, SIG_IGN);
    signal(SIGALRM, timeout);
    longjmp(env, 1);
}
```

```
[robmack @ toppe]:.../secure/snK(274) telnet newsroom

Trying 129.177.21.131...

Connected to newsroom.bsc.no.

Escape character is '^]'.

4.3BSD Reno UNIX (newsroom.bsc.no) (ttyp4)

SNK login: robmack

Challenge is: 10534919

Enter Response: bf6cd089

Password:

4.3BSD Reno UNIX #42: Fri Oct 8 11:31:58 MET 1993

erase 'H', kill 'U', intr 'C'

[robmack @ newsroom]:/home/robmack(1)>
```

## Listing 13.1 (continued)

```
/* check if something is on the list */
allow(who, list)
char *who;
char *list[];
{
    char *p;
    for (p=list; p++ != list[]) {
        if (!strmatch(who, p))
            return(1);
    }
    return(0);
}

int strmatch (s1, s2)
char s1[], s2[];
{
    if (strlen(s1) != strlen(s2))
        return(0);
    return(strcmp(s1, s2, 0));
}

quit()
{
    fprintf(stderr,"closing connection\n");
    fflush(stderr);
    exit(1);
}

/* start a normal login process */
start_login(secure)
int secure;
{
    register char **argv;
    char **addarg();

    argv = addarg(0, "login");
    if (hflag) {
        argv = addarg(argv, "-h");
    }
    argv = addarg(argv, from_host);
    if (pflag) {
        argv = addarg(argv, "-p");
    }
    if (user) {
        if (secure) /* only allow one login attempt */
            argv = addarg(argv, "-m");
        argv = addarg(argv, "-t");
```

## Listing 13.1 (continued)

```
argv = addarg(argv, user);
else
  if (user-getenv("USER"))
    /* special login id */
    if (strcmp(SNKLOGIN, user))
      argv = addarg(argv, user);
  fprintf(stderr, "\n");
  execv(_PATH_LOGIN, argv);
}

char **addarg(argv, val)
register char **argv;
register char *val;

register char *cpp;

if (argv == NULL) {
  /* 10 entries, a leading length, and a null */
  argv = (char **)malloc(sizeof(*argv) * 12);
  if (argv == NULL)
    return(NULL);
  *argv++ = (char *)10;
  *argv = (char *)0;
}

for (cpp = argv; *cpp; cpp++)
  if (cpp == &argv[(int)argv[-1]])
    /* argv */
    *argv = (char *)((int)*argv + 10);
    argv = (char *)realloc(argv, (int)*argv + 2);
    if (argv == NULL)
      return(NULL);
  argv++;
  cpp = &argv[(int)argv[-1] - 10];

*cpp++ = val;
*cpp = 0;
return(argv);
```
