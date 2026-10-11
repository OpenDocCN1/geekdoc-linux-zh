The functions return -1 upon end-of-file or error. The strings hold the terminating newline or delimiter (if there was one), as well as a terminating zero byte. Using getline() is easy, as shown in ch03-getline.c:

```
/* ch03-getline.c -- demonstrate getline(). */
#define _GNU_SOURCE 1
#include <stdio.h>
#include <sys/types.h>

/* main --- read a line and echo it back out until EOF. */
int main(void)
{
    char *line = NULL;
    size_t size = 0;
    ssize_t ret;
    while ((ret = getline(& line, & size, stdin)) != -1)
        printf("(%lu) %s", size, line);
    return 0;
}
```

Here it is in action, showing the size of the buffer. The third input and output lines are purposely long, to force getline() to grow the buffer; thus, they wrap around:

![](bbox=[0.1, 0.58, 0.9, 0.75])

# ### 3.2.2 String Copying: strdup()

One extremely common operation is to allocate storage for a copy of a string. It’s so common that many programs provide a simple function for it instead of using inline code, and often that function is named strdup():