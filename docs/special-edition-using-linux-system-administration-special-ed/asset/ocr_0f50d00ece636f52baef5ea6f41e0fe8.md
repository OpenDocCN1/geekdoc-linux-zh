```
mail.foo.edu    internet address = 192.168.1.4
mail2.foo.edu   internet address = 192.168.1.5
fake.foo.edu    internet address = 192.168.1.1
```

A start of authority record for a domain can also be obtained using the set type command:

```
> set type=soa
> foo.org.
Default Server:  fake.foo.edu.
Address:  192.168.1.1
foo.org
        origin = fake.foo.edu
        mail addr = hostmaster.foo.edu
        serial = 1999042800
        refresh = 28800 (8H)
        retry   = 7200 (2H)
        expire  = 604800 (1W)
        minimum ttl = 86400 (1D)
foo.edu name server = fake.foo.edu
fake.foo.edu    internet address = 192.168.1.1
```

> > **Note**
> >
> > In some of the examples in this section, you will notice that the responses to queries include the Non-authoritative answer indicator. This indicates that the name server had the data in its cache and is returning this data instead of querying the name server for the domain or host being queried.

You can obtain extra debugging information about a query by using the debug or d2 option:

```
> set d2
> cnn.com.
Server:  bwc.bwc.org
Address:  192.115.144.1

;; res_nmkquery(QUERY, cnn.com, IN, A)
-----------------
Got answer:
        HEADER:
                opcode = QUERY, id = 59442, rcode = NOERROR
                header flags:  response, want recursion, recursion avail.
                questions = 1, answers = 18, authority records = 0, additional = 0
        QUESTIONS:
                cnn.com, type = A, class = IN
        ANSWERS:
        -> cnn.com
                internet address = 207.25.71.199
                ttl = 280 (4m40s)
        -> cnn.com
                internet address = 207.25.71.5
                ttl = 280 (4m40s)
        -> cnn.com
                internet address = 207.25.71.6
                ttl = 280 (4m40s)
```