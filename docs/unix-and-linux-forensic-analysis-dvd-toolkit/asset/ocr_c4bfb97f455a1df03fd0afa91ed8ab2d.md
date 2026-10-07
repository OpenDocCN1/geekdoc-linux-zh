# Figure 4.5 Keyword Search

![](bbox=[0.117, 0.075, 0.882, 0.495])

```
```
$ which nc -dev table help
347016 : no more than memory requires, truncating
347017 : /usr/bin/nc --help: respect/help:bounce-hlo
347022 : /usr/lib/buildid/build-linux-gnu-2.6.28-22/truncate.c
347023 : <allocation failed to output stream> smalloc(size)=to increase
347024 : /usr/lib/buildid/build-linux-gnu-2.6.28-22/swaps.h
347025 : size
340912 : higher bounce pool size: ld pages
350710 : /usr/lib/buildid/build-linux-gnu-2.6.28-22/include/bitspool.h
350711 : no bounce
350712 : /usr/lib/buildid/build-linux-gnu-2.6.28-22/include/quantaux.h
350714 : <locks delete lock fault> fmap: no wg
350715 : /usr/lib/buildid/build-linux-gnu-2.6.28-22/include/module.h
350718 : /usr/lib/buildid/build-linux-gnu-2.6.28-22/include/bin/bixe.h
350719 : to mount
351082 : VRK group id is incomplete (ndmx2)
350375 : findmap complete
350376 : fuzzy_cache
354001 : yptr
354819 : Energy sync complete
350678 : port_datagram
350679 : sysctl
356804 : <include duplicate or inacceptable mount options
356805 : /usr/lib/buildid/build-linux-gnu-2.6.28-22/include/fs.h
357035 : <security>: avxtbd truncated entry
357121 : avxtbd: truncated source
357122 : avxtbd: truncated source type
357123 : avxtbd: truncated list
357198 : avxtbd: truncated table
357224 : <security>: list: truncated range
357225 : <security>: truncated list
357368 : <security>: class ID is incorrect, found but should be bs
357294 : <security>: length of class id is has incorrect value
357418 : <security>: the definition of a class is incorrect
357419 : retry_error
357420 : retry_async async
356842 : vfs
```
```

As you see, the search for the term "nc" yielded every entry in the letters "n" and "c" appeared. This is obviously not a very clean search, so I will have to refine my parameters to give me something a bit more usable.

Using what I know about netcat, it can either be used to send or receive information.

```
nc <host.example.com> (or IP address) <port> < infile
```

The command structure to receive a file:

```
nc -l (for *listen*) <port> > outfile
```

Based on this information, I can refine my search to see if the host I am has been used to send or receive a file using netcat. In Figure 4.6, I will show that my search argument did not yield any hits, I can safely assume that the host did not receive any files using "nc -l".