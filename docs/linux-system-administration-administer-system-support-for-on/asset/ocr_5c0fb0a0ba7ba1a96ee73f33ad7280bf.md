```
)
return 0;
}

asmmlinkage int sys_settimer(int which, struct itimeral *value, struct itimeral *ovalue)
{
    int error;
    struct itimeral set_buffer, get_buffer;

    if (value) {
        error = verify_area(VERIFY_READ, value, sizeof(*value));
        if (error)
            return error;
        memcpy_fromfs(&set_buffer, value, sizeof(set_buffer));
    } else
        memset((char *) &set_buffer, 0, sizeof(set_buffer));

    if (ovalue) {
        error = verify_area(VERIFY_WRITE, ovalue, sizeof(struct itimeral));
        if (error)
            return error;
    }
```

The following code is the error handling. Because there is an issue with possible buffer overflows, the error handling checks for it.

```
error = _settimer(which, &set_buffer, ovalue ? &get_buffer : 0);
if (error || !ovalue)
    return error;

memcpy_tofs(oalue, &get_buffer, sizeof(get_buffer));
return error;
}
```

> **Buffer overflows have become a way to exploit a Linux system. They are covered from a security viewpoint in Chapter 9.**