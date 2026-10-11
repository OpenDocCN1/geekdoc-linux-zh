scratch. If clearenv() is not available, the GNU/Linux clearenv(3) manpage recommends using ‘environ = NULL;’ to accomplish the task.

# 2.4.2 The Entire Environment: environ

The correct way to deal with the environment is through the functions described in the previous section. However, it’s worth a look at how things are managed “under the hood.”

The external variable environ provides access to the environment in the same way that argv provides access to the command-line arguments. You must declare the variable yourself. Although standardized by POSIX, environ is purposely not declared by any standardized header file. (This seems to evolve from historical practice.) Here is the declaration:

```
extern char **environ; /* Look Ma, no header file! */ POSIX
```

Like argv, the final element in environ is NULL. There is no “environment count” variable that corresponds to argc, however. This simple program prints out the entire environment:

```
/* ch02-printenv.c --- Print out the environment. */
#include <stdio.h>

extern char **environ;

int main(int argc, char *argv)
{
 int i;

 if (environ != NULL)
 for (i = 0; environ[i] != NULL; i++)
 printf("%s\n", environ[i]);

 return 0;
}
```

Although it’s unlikely to happen, this program makes sure that environ isn’t NULL before attempting to use it.

Variables are kept in the environment in random order. Although some Unix shells keep the environment sorted by variable name, there is no formal requirement that this be so, and many shells don’t keep them sorted.