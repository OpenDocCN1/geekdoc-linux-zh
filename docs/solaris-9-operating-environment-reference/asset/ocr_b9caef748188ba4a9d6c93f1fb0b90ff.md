# fnrename 389

# fnrename — Rename the Binding of an FNS Name

Synopsis
/usr/bin/fnrename [-s] [-v] context-name old-atomic-name new-atomic-name

Description
fnrename renames the Federated Naming Service (FNS) binding of old-atomic-name to new-atomic-name in the context of context-name. Both old-atomic-name and new-atomic-name must be atomic names, to be resolved in the context by context-name.

+   Options
-s Overwrite any reference already bound to new-atomic-name. If you omit this option, fnrename fails if new-atomic-name is already bound.
-v Display the binding being renamed.

Examples
The following example binds calendar to the reference bound to clendar in the context named by/usr/jsmith/service/ unbinds clendar.
castle% fnrename user/jsmith/service/ clendar calendar

Attributes
See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
 Availability | SUNwns |

See Also
fnbind(1), flist(1), fnunbind(1), fncreate(1M), fdestroy(1M), xfn_links(3N), attributes(5), fns(5), fns_references(5)

# fnsearch — Search for FNS Objects with Specified Attributes

Synopsis
/usr/bin/fnsearch [-Allv] [-n max] [-s scope] composite-name [-a ident]... [-O | -U] filter-expr [filter-arg]...

Description
The fnsearch command displays the names and, optionally, the attributes and references of Federated Naming Service (FNS) objects bound at or below composite-name whose attributes satisfy a given filter expression. Specify the filter