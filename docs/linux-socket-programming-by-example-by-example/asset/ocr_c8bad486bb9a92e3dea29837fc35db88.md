# **CAUTION**

The pointer returned by getprotoent(3) is only valid until the next call to the same function.

![](bbox=[0.06, 0.18, 0.22, 0.35])

# **Listing 7.4: The struct protoent Structure**

```
```
struct protoent {
  char    *p_name; /* official protocol name */
  char    **p_aliases;   /* alias list */
  int     p_proto;   /* protocol number */
}
```
```

The structure members are more fully described as follows:

+   - The structure member **p_name** contains a pointer to a C string that names the protocol (for example “tcp”).
+   
+   - The member **p_aliases** is a pointer to an array of C string pointers, of which the last entry is a NULL pointer. If pp points to this structure, then pp->p_aliases[0] contains the first C string (or is NULL when there are no aliases). An example of an alias might be “TCP” (the uppercase name of the protocol is often specified as an alias).
+   
+   - The member **p_proto** contains the protocol number. For example, the protocol number found in */etc/protocols* for entry “tcp” should agree with the C macro constant IPPROTO_TCP. If you check with */usr/include/netinet/in.h* and with the value in */etc/protocols*, you will indeed see that they both have the value 6.

# **CAUTION**

The getprotoent(3) function suffers from the same flaw as the getservent(3) function under Linux. Even when the value of errno is zeroed prior to calling getprotoent(3), when end-of-file is reached and indicated by a NULL return pointer, the errno value for Red Hat Linux 6.0 is EONENT.

Under other UNIX operating systems, such as HP-UX 10.2 and Sun Solaris 5.5.1, the errno value is left at zero when end-of-file is returned. This leads the author to speculate that this behavior is a bug, which might be corrected in a later release of Linux.

The getprotoent(3) function returns a NULL pointer when end-of-file is reached or when an error has been encountered.

Listing 7.5 shows a demonstration program that iterates through all of the /etc/protocols database entries.