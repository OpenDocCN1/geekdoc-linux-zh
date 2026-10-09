meaningful. As I said in Section 3.5, how they’re encoded in the device ID isn’t standardized, but taking the rightmost 8 bits as the minor number usually works:

```
```
static void print_size(const struct stat *statp)
{
    switch (statp->st_mode & S_IFMT) {
    case S_IFCHR:
    case S_IFBLK:
        printf("%4u,%4u", (unsigned)(statp->st_rdev >> 8),
                (unsigned)(statp->st_rdev & 0xff));
        break;
    default:
        printf("%9lu", (unsigned long)statp->st_size);
    }
}
```
```

Next comes the file data-modification date and time, using the Standard C function $\mathrm{strftime}$ to do the hard work. The functions time and $\mathrm{diff\ time}$ are in Standard C, too. (See Section 1.7.1 for all three.) We don’t normally print the year, unless the time is 6 months away, in which case we skip the time to make room:${ }^{8}$

```
```
static void print_date(const struct stat *statp)
{
    time_t now;
    double diff;
    char buf[100], *fmt;

    if (time(&now) == -1) {
        printf(" ??????????????");
        return;
    }

    diff = diff_time(now, statp->st_mtime);
    if (diff < 0 || diff > 60 * 60 * 24 * 182.5) /* roughly 6 months */
        fmt = "%b %e %Y";
    else
        fmt = "%b %e %H:%M";
    strftime(buf, sizeof(buf), fmt, localtime(&statp->st_mtime));
    printf(" %s", buf);
}
```
```

The last thing we want to print is the file name, which isn’t in the stat structure, of course, because it isn’t in the i-node. It’s a little tricky, however, because if the name is a symbolic link, we want to print both it and its contents:

8. Generally, our policy is to check for all errors except when formatting (for printing) and printing. $\mathrm{diff\ time}$ isn’t an exception—it’s one of those functions that has no error return.