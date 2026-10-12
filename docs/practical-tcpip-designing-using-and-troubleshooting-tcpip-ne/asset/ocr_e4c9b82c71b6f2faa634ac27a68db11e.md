![](bbox=[0.2, 0.08, 0.75, 0.25])

# Common problems with adding and deleting routes

Web Appendix 5 gives a list of error messages and their causes. This section looks at it the other way round and lists the most common mistakes that cause errors.

+   omitting the **gw** keyword when adding a route:

```
route add default            1.2.3.4       wrong
route add default            gw 1.2.3.4      OK
```

+   omitting the **-net** option or the netmask when adding a network route, so you might end up creating a route to a single host instead:

```
route add 10.2.2.0           gw 10.1.1.22    wrong
route add -net 10.2.2.0      gw 10.1.1.22    wrong
route add -net 10.2.2.0/24   gw 10.1.1.22     OK
```

+   specifying a network using one of the host addresses in its range instead of the network address:

```
route add -net 10.2.2.47/24  gw 10.1.1.22    wrong
route add -net 10.2.2.0/24    gw 10.1.1.22    OK
```