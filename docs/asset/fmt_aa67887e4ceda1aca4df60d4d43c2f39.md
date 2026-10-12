
`[libdefaults]`

`ticket_lifetime = 600`

`default_realm = c3.telstra-mm.net.au`

```
** new *
```

`kdc_req_checksum_type = 2`

`ap_req_checksum_type = 2`

`safe_req_checksum_type = 3`

`ccache_type = 2`

```
** end of new *
```

`[realms]`

```
c3.telstra-mm.net.au = {
  kdc = dce-server
  admin_server = dce-server
  default_domain = c3.telstra-mm.net.au
}
```

```
wfh.c3.telstra-mm.net.au = {
  kdc = wfh.c3.telstra-mm.net.au
  admin_server = wfh.c3.telstra-mm.net.au
  default_domain = c3.telstra-mm.net.au
}
```

```
wfh1.c3.telstra-mm.net.au = {
  kdc = wfh1.c3.telstra-mm.net.au
  admin_server = wfh1.c3.telstra-mm.net.au
  default_domain = c3.telstra-mm.net.au
}
```

```
wfh2.c3.telstra-mm.net.au = {
  kdc = wfh2.c3.telstra-mm.net.au
  admin_server = wfh2.c3.telstra-mm.net.au
  default_domain = c3.telstra-mm.net.au
}
```

```
wfh3.c3.telstra-mm.net.au = {
  kdc = wfh3.c3.telstra-mm.net.au
  admin_server = wfh3.c3.telstra-mm.net.au
  default_domain = c3.telstra-mm.net.au
}
```

```
wfh4.c3.telstra-mm.net.au = {
  kdc = wfh4.c3.telstra-mm.net.au
  admin_server = wfh4.c3.telstra-mm.net.au
  default_domain = c3.telstra-mm.net.au
}
```

```
wfh5.c3.telstra-mm.net.au = {
  kdc = wfh5.c3.telstra-mm.net.au
  admin_server = wfh5.c3.telstra-mm.net.au
  default_domain = c3.telstra-mm.net.au
}
```

```
)
```

```
** new *2
```

`[domain_realm]`

`nc3.telstra-mm.net.au = c3.telstra-mm.net.au`

```
** end *2
```
