# Listing 13.1 (continued)

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

# Listing 13.2  snk.h — part of the login wrapper program, snklogin.

```
/* special id which uses prishell */
#define SNKLOGIN "snk"
/* timeout value for prompts (in seconds) */
#define SNKTIMEOUT 180

/* modes that real_ipinfo() will return */
/* return the real hostname on the socket */
#define HOSTNAME 1
/* return the real ip address on the socket */
#define IP_ADDR 2
```