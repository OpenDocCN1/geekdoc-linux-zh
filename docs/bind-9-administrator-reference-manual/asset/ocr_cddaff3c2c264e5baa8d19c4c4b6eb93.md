# Chapter 6. BIND 9 Configuration Reference

In the following example, any queries received from any of the addresses of the host itself will get responses preferring addresses on any of the locally connected networks. Next most preferred are addresses on the 192.168.1/24 network, and after that either the 192.168.2/24 or 192.168.3/24 network with no preference shown between these two networks. Queries received from a host on the 192.168.1/24 network will prefer other addresses on network to the 192.168.2/24 and 192.168.3/24 networks. Queries received from a host on the 192.168.4/24 or the 192.168.5/24 network will prefer other addresses on its directly connected networks.

```
sortlist {
    localhost;
    localnets;
        192.168.1/24;
        { 192.168.2/24; 192.168.3/24; }; // IF the local host
    192.168.1/24; // THEN first fit on the
    { 192.168.1/24;
        { 192.168.2/24; 192.168.3/24; }; }; // following nets
    192.168.2/24;
    { 192.168.1/24; 192.168.3/24; }; }; // IF on class C 192.168.1
    192.168.2/24;
// THEN use .1, .2 or .3
    { 192.168.1/24; 192.168.3/24; }; };; // IF on class C 192.168.2
    192.168.3/24;
    { 192.168.1/24; 192.168.2/24; }; };; // THEN use .2, .1 or .3
    { 192.168.4/24; 192.168.5/24; }; }; // IF on class C 192.168.3
fer that net
    ; // if .4 or .5, pre-
};
```

The following example will give reasonable behavior for the local host and hosts on directly connected networks. It is similar to the behavior of the address sort in BIND 4.9.x. Responses sent to queries from the local host will favor any of the directly connected networks. Responses sent to queries from other hosts on a directly connected network will prefer addresses on that same network. Responses to other queries will not be sorted.

```
sortlist {
    {localhost; localnets};
    {localnets};
};
```

74