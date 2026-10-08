# crle 189

The following example creates an alternative object cache for an ELF executable.

```
example$ crle -c /local/$HOST/.xterm/ld.config -f RTLD_REL_REL
-o /usr/openwin/bin/xterm
example$ in -s /usr/local/$.xterm/xterm /local/$HOST/xterm
example$ ldd /usr/local/$HOST/xterm
libXaw.so.5 => /local/$HOST/.xterm/libXaw.so.5 (alternate)
libXmu.so.4 => /local/$HOST/.xterm/libXmu.so.4 (alternate)
ibc.so.1 => /local/$HOST/.xterm/libc.so.1 (alternate)
```

With this configuration, a new xterm and its dependencies are created. These new objects are fully relocated to themselves and result in faster startup than the originating objects.

> Note — The execution of this application uses its own configuration file. Using this model is generally more flexible than using the environment variable LD_CONFIG, because the configuration file is not erroneously used by other applications as ldd(1) or truss(1).

The following example creates an alternative object cache to replace an ELF object.

```
example$ ldd /usr/sbin/bin/vold
libthread.so.1 => /usr/lib/libthread.so.1

example$ crle -a /usr/lib/libthread.so.1 -o /usr/lib/lwp
example$ crle
```

Configuration file [2]: /var/ld/ld.config
Default Library Path (ELF): /usr/lib (system default)
Trusted Directories (ELF): /usr/lib/secure (system default)

```
Directory: /usr/lib
libthread.so.1 (alternate: /usr/lib/lwp/libthread.so.1)
...
example$ ldd /usr/sbin/bin/vold
libthread.so.1 => /usr/lib/lwp/libthread.so.1 (alternate)
...
example$ .
```

With this configuration, any dependency that would normally resolve to /usr/lib/libthread.so.1 instead resolves to /usr/lib/lwp/libthread.so.1. See threads(3THR).

# Exit Status

The creation or display of a configuration file returns 0; otherwise, any error condition is accompanied by a diagnostic message and a non-zero value is returned.