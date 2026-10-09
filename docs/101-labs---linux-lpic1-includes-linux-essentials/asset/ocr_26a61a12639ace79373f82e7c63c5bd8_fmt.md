
There are many more options available, most of which you will probably never need--but, as always, the man page is worth a skim.

## Task 3

Not to be outdone, `host` can do many of the same things that `dig` can:

+ `host -v -t A 1011abs.net`
+ `host -t MX 1011abs.net`
+ `host -v -t CNAME www.1011abs.net [dns1]`
+ `host -t AAAA example.com [dns2]`

See the similarities?

## Task 4

By default, Ubuntu 18.04 uses a local caching nameserver. If you run a non-recursive query on this (with the `dig` option `+norecurse`), it will come up empty:

```
dig 1011abs.net +norecurse 127.0.0.53
```

Run this on one of your main nameservers and it will work.

## Notes

`resolvconf` is a tool that was previously used in Ubuntu to manage `resolv.conf`. No longer installed by default, it seems to have been superseded by `systemd-resolved`.

For some users, the `dig` and `host` commands for the `AAAA` record required `www` before the `example` address.
