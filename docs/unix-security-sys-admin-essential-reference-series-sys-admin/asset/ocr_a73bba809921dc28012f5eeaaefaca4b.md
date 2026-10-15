# Listing 15.2 The server passwd program executes /bin/passwd with a username, and has /bin/passwd prompt for the new password.

```
/*
 * passwd -- the daemon that looks after changing passwords
 * from afar. Run as a login shell, passed the userid via
 * the TERM environment variable.
 */
#include
#include

char *ProgName;
#define ERR (-1)
#define YES 0
#define NO 1
#define MAXLINE 255

/*ARGSUSED*/
main(argc, argv) int argc; char *argv[]; {
    char *remoteName, *getenv();
    struct passwd *p, *getpwnam();
    unsigned short getuid(), geteuid();
    int rc;

    ProgName = argv[0];
    (void) fprintf(stderr,"Connected to passwd server...\n");
    /* Become root if you aren't already. */
    if (seteuid(0) != geteuid()) == ERR ) {
        (void) fprintf(stderr,"%s: unable to change to root, halting\n", ProgName);
        (void) exit(1);
    }

    if ((remoteName=getenv("TERM")) == NULL) {
        (void) fprintf(stderr,"%s: no TERM variable supplied, halting\n", ProgName);
        (void) exit(1);
    }
    if ((p= getpwnam(remoteName)) == NULL) {
        (void) fprintf(stderr,"%s: no userid %s known, halting\n", ProgName,remoteName);
        (void) exit(1);
    }
```