anything the specified name server tells it. You use this item in one of the two following configurations:

```
bogus yes;
bogus no;
```

Next, you can secure your zone files somewhat by using a **keys** setting. You already have to have set up a **key** statement elsewhere. After you have, use the following to implement key-based authentication:

```
keys {
keyID1
keyID2
...
keyIDn
};
```

# The Zone Files

A DNS zone file is where you specifically lay out which IP addresses map to which hosts, and other useful information such as the primary mail servers for your domain. Each entry in this file is called a *resource record*. What types of records, and how many, depend on which zone file you are setting up. This information is given in the context of the tasks in the Immediate Solutions section. This section covers the theory underlying how the file is laid out. One interesting thing to note is that zone files are the same regardless of the operating system you are using. They have to be, because you never know what operating system the organization providing your backup DNS runs its name service under.

A zone file begins with the Start of Authority (SOA) record, which is what you use to lay out overall information about the zone before you get into the details. This statement is laid out in the following manner:

```
@ IN SOA domain.extension. admin.domain.ext. (
serial_number
refresh
retry
expire
minimum )
```

The parts that you do not change are:

+   - @—The zone’s name. The @ is a self-referential wildcard—meaning that it stands for the default domain name.