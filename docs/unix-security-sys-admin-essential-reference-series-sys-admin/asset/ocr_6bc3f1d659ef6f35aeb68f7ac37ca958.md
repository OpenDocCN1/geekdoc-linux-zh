# Listing 15.4 The client ccopy program is used in the client password update script.

```
/*
 * ccopy - copy only if the target file does not exist. Used
 * to avoid race conditions. This is a classical unix
 * lock file creation mechanism: it's an atomic action.
 */
#include 
#include  /* For open(2). */
#include  /* For umask and fstat(2). */
#include 
#include  /* For error reporting. */
extern int sys_nerr;
extern char *sys_errlist[];

#define USERRR 1  /* Parameters messed up or missing. */
#define EXISTS 2  /* File exists, try again later. */
#define REALERR 3  /* Something bad happened. */
#define ERR (-1)  /* System's normal error value. */

char *ProgName = NULL; /* Name (ie, ccopy) for error reports. */
main(argc, argv) int argc; char *argv[]; {
    ProgName = argv[0];
    if (argc != 3) {
        (void) fprintf(stderr, "%s: Error - you must supply
        exactly two filenames.\n", ProgName);
        (void) fprintf(stderr, "%s - copy one file to another
        IFF the second doesn't exist\n", ProgName);
        (void) fprintf(stderr, "Usage: %s infile outfile\n",
        ProgName);
        exit(USERRR);
    }
    exit(ccopy(argv[1],argv[2]));
    /*NOTREACHED*/
}
```