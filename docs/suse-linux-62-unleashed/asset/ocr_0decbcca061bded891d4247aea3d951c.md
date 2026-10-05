# Networking and Internet Services
PART II

/* C style comments can comment out multiple lines /
// C++ style comments comment one or fractional lines
# Shellscript style comments function like C++ style

Other statements take the form

keyword {statement; statement; ... statement;}

Because everything in this file is brace, space-, and semicolon-delimited, multiple spacing\and line breaks do not affect its functionality.

# Caution

Bugs caused by syntax errors in the named files are hard to detect. Often there are
no symptoms, and even when symptoms are observable, the messages are often
crypt and hard to trace to the bug. So it is imperative to check the files carefully.

The two most common section-starting keywords in named.conf are options and zone.
Listing 8.5 is a named.conf that does reverse DNS on its loopback and its eth0, and does
forward DNS on domain.cxm.

# LISTING 8.5 The Example named.conf File

```
options {
    directory "/var/named";      #referred files in /var/named
}

zone "." {\ #hints for caching
    type hint;
    file "named.ca";               #root servers file in
                             # /var/named/named.ca
}

zone "0.0.127.in-addr.arpa" { #reverse on loopback
    type master;
    file "named.local";
}

zone "42.168.192.in-addr.arpa" { #reverse on eth0 subnet
    type master;\                   #file is on this host
    file "named.192.168.142";      #rev dns file
};
```