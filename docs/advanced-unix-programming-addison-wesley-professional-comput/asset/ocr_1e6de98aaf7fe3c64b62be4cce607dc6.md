| Option | Description |
| :--- | :--- |
| SO_REUSEADDR | bind allows reuse of local addresses. Otherwise, bind returns −1 with errno set to EADDRINUSE if a previous bind has occurred within a system-defined period (for example, a few minutes). Very convenient for debugging and testing. (Bsg) |
| SO_SNDBUF | Send buffer size. This option takes an int value. (Isg) |
| SO_SNDLOWAT | Send low-water mark. Nonblocking send operations (e.g., write) send no data unless the lesser of this amount and the requested amount can be sent immediately. (Isg) |
| SO_SNDTIMEO | Uses a timeval structure (Section 1.7.1) for the maximum time to wait for a blocking send operation to complete. Zero time (the default) means infinite. If the time expires, the operation returns with a partial count or with −1 and errno set to EAGAIN or EWOULDBLOCK. (Xsg) |
| SO_TYPE | Socket type (e.g., SOCK_STREAM). (Isg) |

To show how these options are used with `getsockopt`, here’s a program that displays the values for several different kinds of sockets:

```
```c
typedef enum (OT_INT, OT_LINGER, OT_TIMEVAL) OPT_TYPE;

static void show(int skt, int level, int option, const char *name,
OPT_TYPE type)
{
    socklen_t len;
    int n;
    struct linger lng;
    struct timeval tv;

    switch (type) {
    case OT_INT:
        len = sizeof(n);
        if (getsockopt(skt, level, option, &n, &len) == -1)
            printf("%s FAILED (%s)\n", name, strerror(errno));
        else
            printf("%s = %d\n", name, n);
        break;
    case OT_LINGER:
        len = sizeof(lng);
        if (getsockopt(skt, level, option, &lng, &len) == -1)
            printf("%s FAILED (%s)\n", name, strerror(errno));
```
```