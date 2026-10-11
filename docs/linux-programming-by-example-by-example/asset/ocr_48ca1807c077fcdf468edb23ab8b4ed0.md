```
printf("%s\n", msg_hi);
prm sg(msg_bye);
return 0;
}
msg.h
```

```
/*
* msg.h Header for msg.c
*/

#ifndef MSG_H
#define MSG_H

void prmsg(char *msg);

*endif /* MSG_H */
```

```
msg.c
/*
* msg.c - Define function from msg.h
*/
#include <stdio.h>
#include "msg.h"

void prmsg(char *msg)
{
    printf("%s\n", msg);
}
```

The command to compile these programs, and thus to create newhello, is

```
$ gcc msg.c showt.c -o newhello
```

Running this program, the output is

![](bbox=[0.04, 0.68, 0.16, 0.73])

# **Output**

```
$ ./newhello
Hi there, programmer!
Goodbye, programmer!
```

gcc goes through the same preprocess-compile-link steps as before, this time creating object files for each source file before creating the binary,