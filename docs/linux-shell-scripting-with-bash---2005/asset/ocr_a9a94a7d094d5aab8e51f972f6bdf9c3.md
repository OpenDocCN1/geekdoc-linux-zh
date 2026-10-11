One common mistake when using putenv is reusing the string assigned to the environment. The command actually creates a pointer to the string being assigned; it does not copy the string into the environment. Running a command such as `putenv(s)` means that the string `s` must be untouched until it is removed from the environment.

For a simple variable sharing example, suppose you created a script called `c_script.sh` to multiply a variable called `COUNT` by the first script argument, as shown in Listing 18.3.

# **Listing 18.3** c_script.sh

```
```
#!/bin/bash
#
# c_script.sh: an example of exporting a C variable to a script

shopt -s -o nounset
let "COUNT=COUNT*$1"
echo "$COUNT"

exit 0
```
```

The script assumes the variable `COUNT` exists.

```
```
$ declare -ix COUNT=4
$ bash c_script.sh 3
12
```
```

Using putenv and popen, a C variable can be copied to the environment, and a new value for the variable can be read from the pipe, as shown in Listing 18.4.

# **Listing 18.4** c_script.c

```
```
/* c_script.c: run a script from C using popen */

#include <stdio.h>
#include <stdlib.h>

int main() {

    FILE *f = NULL;                /* the pipe file */
    char env_count[255] = "";      /* string buffer for COUNT */
    int count = 5;                 /* C variable count */

    /* Declare COUNT in the environment */

    sprintf(env_count, "COUNT=%d", count);  /* declare env var */
    putenv(env_count);                  /* export it */
```
```