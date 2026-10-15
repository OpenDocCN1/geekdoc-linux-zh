
Now, if you type that command as-is, your DNS will break, because, of course, those addresses aren’t real DNS servers. You can substitute the IP addresses for real public nameservers if you like.

In either case, you’ll probably want to switch back to what you had before:

```
systemd-resolve --set-dns=[dns1] --set-dns=[dns2] --interface=[interface]
```

Notes: `systemd-resolve` can also be used to make DNS queries a la `dig`, but its options for this are much more limited.
