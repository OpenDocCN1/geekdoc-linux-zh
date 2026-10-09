```
zone "0.168.192.in-addr.arpa" IN {
type master;
file "named.local";
notify YES;
};
zone "." IN {
type hint;
file "named.ca";
};
// end local view
view "public" IN {
// start public view
match-clients { "any";};
recursion NO;
zone "zach.net" IN {
type master;
file "public.net";
notify YES;
};
zone "0.168.192.in-addr.arpa" IN {
type master;
file "named.public";
notify YES;
};
zone "." IN {
type hint;
file "named.ca";
};
// end public view
logging{
channel "misc" {
file "/var/log/bind/misc2.log" versions 2 size 1m;
print-time YES;
print-severity YES;
print-category YES;
};
category default {
"misc";
};
//end logging
```

The ordering of View clauses within **named.conf** is critical because the view that is presented to a client is the first view that the client matches. The preceding **named.conf** file holds two View clauses: one for local users and one for public users, in that order. Local users are defined to be those on the 192.168.0.0/24 subnet or localhost (127.0.0.1); public users are defined to be any users. If you reversed the