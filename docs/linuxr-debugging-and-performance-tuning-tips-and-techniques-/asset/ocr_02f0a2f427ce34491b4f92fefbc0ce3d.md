```
1906 if ((pid = fork()) < 0) { 1907 save_errno = errno; 1908 close(ptoc[0]); close(ptoc[1]); 1909 close(ctop[0]); close(ctop[1]); 1910 errno = save_errno; 1911 return FALSE; 1912 }
```

Lines 1906–1912 fork the child, this time closing both pipes if `fork()` failed. Here too, the original `errno` value is saved and restored for later use in producing a diagnostic.

```
1914 if (pid == 0) { /* child */ 1915 if (close(1) == -1) 1916 fatal(_("close of stdout in child failed (%s)*), 1917 strerror(errno)); 1918 if (dup(ctop[1]) != 1) 1919 fatal(_("moving pipe to stdout in child failed (dup: %s)*), 1920 strerror(errno)); 1921 if (close(0) == -1) 1922 fatal(_("close of stdin in child failed (%s)*), 1923 strerror(errno)); 1924 if (dup(ptoc[0]) != 0) 1925 fatal(_("moving pipe to stdin in child failed (dup: %s)*), 1926 strerror(errno)); 1927 if ( close(ptoc[0]) == -1 || close(ptoc[1]) == -1 || close(ctop[0]) == -1 || close(ctop[1]) == -1) 1928 fatal(_("close of pipe failed (%s)*), strerror(errno)); 1929 /* stder does NOT get dup'ed onto child's stdour */ 1930 exec(*/bin/sh", "sh", "-c", &* arg, NULL); 1931 _exit(errno == ENOENT ? 127 : 126); 1932 }
```

Lines 1914–1931 handle the child's code, with appropriate error checking and messages at each step. Line 1915 closes standard output. Line 1918 copies the child-to-parent pipe write end to 1. Line 1920 closes standard input, and line 1923 copies the parent-to-child read end to 0. If this all works, the child's standard input and output are now in place, connected to the parent.

Lines 1925–1928 close all four original pipe file descriptors since they're no longer needed. Line 1928 reminds us that standard error remains in place. This is the best decision, since the user will see errors from the coprocess. An awk program that must capture standard error can use the `"2>&1"` shell notation in the command to redirect the coprocess's standard error or send it to a separate file.

Finally, lines 1929–1930 attempt to run `exec()` on the shell and exit appropriately if that fails.