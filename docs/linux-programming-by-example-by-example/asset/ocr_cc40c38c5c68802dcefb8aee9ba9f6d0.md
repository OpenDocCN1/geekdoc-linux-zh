# Example

![](bbox=[0.04, 0.1, 0.2, 0.16])

# Example

The following program is a problem child beset with memory bugs, including the following:

+   • Has a memory leak
+   • Overruns the end of dynamically allocated heap memory
+   • Underruns a memory buffer
+   • Frees the same buffer twice
+   • Accesses freed memory
+   • Overwrites statically allocated stack and global memory

```
/*
 * badmem.c-- Demonstrate usage of memory debugging tools
 */
#include <stdlib.h>
#include <stdio.h>
#include <string.h>

char g_buf[5];                       /* global buffer */

int main(void)
{
   char *buf;
   char *leak;
   char l_buf[5];                   /* local buffer */

   /* Won't free this */
   leak = malloc(10);

   /* Overrun buf a little bit */
   buf = malloc(5);
   strcpy(buf, "abcde");
   printf("LITTLE : %s\n", buf);
   free(buf);

   /* Overrun buf a lot */
   buf = malloc(5);
```