```
```text
EC_CLEANUP_BGN
    if (dirfd != -1) {
        (void)fchdir(dirfd);
        (void)close(dirfd);
    }
    if (sp != NULL)
        (void)closedir(sp);
    return result;
EC_CLEANUP_END
)
```
```

do_dir is where the recursion takes place. It opens _dirfd_ to the current directory so it can be restored on cleanup. Then it opens the directory with _opendir_ and changes to it so the entries can be processed relative to their parent directory. It's very common to get an _EACCES_ error because a directory isn't readable (_opendir_ fails) or not searchable (_chdir_ fails), so we just want to print a message in those cases—not terminate processing.

Next, if the _-R_ argument was specified, we tell the callback function to print the current directory path. This is so all normal printing can be localized to one callback function.

Then we have the Pass 1 _readdir_ loop (in which _do_entry_ is called with _stat_only_ set to true), a _rewinddir_ system call, and, if _-R_ was specified, the Pass 2 _readdir_ loop (calling _do_entry_ with _stat_only_ set to false). The recursion occurs because a Pass 2 call to _do_dir_ might call _do_dir_ recursively. Note that both _readdir_ loops skip the _._ and _.._ entries, which _ls_ also omits by default.

We decided to treat errors from _readdir_ as nonfatal, to keep things going, rather than bailing out with the _ec_nzero_ macro, which explains the two calls to _syserr_print_, which is:

```
```c
void syserr_print(const char *msg)
{
    char buf[200];

    fprintf(stderr, "ERROR: %s\n", syserrmsg(buf, sizeof(buf), msg,
      errno, EC_ERRNO));
}
```
```

_syserrmsg_ was in Section 1.4.1.

That's it—our own fully recursive version of _ls_!