```
zone  "1.168.192.in-addr.arpa" {
```

```
    type  master;
```

```
    file  "named.rev";
```

```
};
```

```
//
```

```
// our secondary information for example.com
```

```
//
```

```
zone  "example.com" {
```

```
    type  slave;
```

```
    file  "example.com.cache";
```

```
    masters { 10.0.0.1; 10.0.0.2; };
```

```
};
```

# Here is the /var/named/named.ca file:

```
;  This file holds the information on root name servers needed to
```

```
;  initialize cache of Internet domain name servers
```

```
;  (e.g. reference this file in the \`cache   .file\`
```

```
;  configuration file of BIND domain name servers).
```

```
;
```

```
;  This file is made available by InterNIC registration services
```

```
;  under anonymous FTP as
```

```
;
```

```
          file            /domain/named.root
```

```
          on server       FTP.RS.INTERNIC.NET
```

```
          -OR- under Gopher at  RS.INTERNIC.NET
```

```
;
```

```
          under menu      InterNIC Registration Services (NSI)
```

```
              submenu     InterNIC Registration Archives
```

```
                  file    named.root
```

```
;
```

```
;
```

```
          last update:     Aug 22, 1997
```

```
          related version of root zone: 1997082200
```

```
;
```

```
;  formerly NS.INTERNIC.NET
```

```
;
```

```
.
```