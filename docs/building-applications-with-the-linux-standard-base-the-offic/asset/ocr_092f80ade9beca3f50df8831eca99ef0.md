```
Example 3.1: Using gettext()

```c
#include <stdio.h>
#include <locale.h>
#include <libintl.h>

int
main(int argc, char *argv[])
{
printf("LANG=%s\n", getenv("LANG"));

/* initialize LC_MESSAGES according to
 * LC_ALL, LC_MESSAGES, or LANG
 */

setlocale(LC_ALL, "");

printf ("dirname=%s\n",
bindtextdomain("ghw", "/usr/share/locale/"));

printf("domainname=%s\n", textdomain("ghw"));

/* Look up MSGID in the current default message catalog for the
 * current LC_MESSAGES locale. If not found, gettext() returns
 * MSGID itself (the default text).
 */

printf(gettext("Hello World\n"));

printf(gettext("The value of Open Standards \
is only evident to Open Minds\n"));

printf(gettext("Good Bye\n"));

exit(0);
}
```
```