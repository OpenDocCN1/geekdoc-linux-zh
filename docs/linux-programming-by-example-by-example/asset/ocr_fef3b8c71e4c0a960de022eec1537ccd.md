```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
#include <pwd.h>

int main(void)
{
    char *login;
    struct passwd *pentry;

    /* Get the login name */
    if((login = getlogin()) == NULL) { /* oops */
        perror("getlogin");
        exit(EXIT_FAILURE);
    }
    printf("getlogin returned %s\n", login);

    /* get the password entry for login */
    if((pentry = getpwnam(login)) == NULL) {
        perror("getpwnam");
        exit(EXIT_FAILURE);
    }
    /* display the full name */
    printf("gecos: %s\n", pentry->pw_gecos);

    exit(EXIT_SUCCESS);
}
```

# Output

```
$ ./getname
getlogin returned kwall
gecos: Kurt Wall
```

The `if` statements guard against the possibility of `getlogin` or `getpwnam` returning `NULL`. If either function returns `NULL`, `perror` will print an error message and the program exits. First, the program uses `getlogin` to retrieve and display the login name running the program. Then, it uses that name to retrieve the password entry and displays the user's full name (stored in the GECOS field of `/etc/passwd`—see man 5 passwd for more information).