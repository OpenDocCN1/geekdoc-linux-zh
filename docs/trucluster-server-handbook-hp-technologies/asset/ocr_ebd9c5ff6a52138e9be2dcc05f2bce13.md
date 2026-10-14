```
```text
[500] sys.unix.clu.caa.app.error
[500] sys.unix.clu.caa.app.modified
[500] sys.unix.clu.caa.res.modified
[500] sys.unix.clu.caa.res.registered
[500] sys.unix.clu.caa.res.unregistered
```
```

CAA also has the following predefined event filters.

```
```text
# evf -vd /usr/share/evm/filters caa clu
> | awk '/evf|^/ { print "^", $1, "> next" } /caa/ { print }'

/usr/share/evm/filters

caa.evf
    @caa:caa              -> [name sys.unix.clu.caa]
    @caa:app              -> [name sys.unix.clu.caa.app]
    @caa:cli              -> [name sys.unix.clu.caa.cli]
    @caa:err              -> [name sys.unix.clu.caa.err]
    @caa:res              -> [name sys.unix.clu.caa.res]

clu.evf
    @clu:caa              -> [name sys.unix.clu.caa]
```
```

Incidentally, the following command is sufficient. We added the awk line to make the output more compact and to filter out any filters not specifically CAA-related.

```
```text
# evf -vd /usr/share/evm/filters clu caa
```
```

The evf(1) command was written for the *TruCluster Server Handbook* and is not part of the *TruCluster Server* or *Tru64 UNIX* software distribution. See the book’s web site to download – Appendix B contains the URL.

# 23.8  References

+   - The *TruCluster Server* Cluster Technical Overview.
+   - The *TruCluster Server* Cluster Highly Available Applications.
+   - Reference pages (noted within the text).