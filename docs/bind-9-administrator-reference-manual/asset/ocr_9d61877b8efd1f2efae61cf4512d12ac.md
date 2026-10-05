present. The update-policy statement only examines the signer of a message; the source address is not relevant.

This is how rule definition looks:

( grant | deny identity nametype name [ types ]

Each rule or denies privileges. Once a message has successfully matched a rule, the operation is immediately granted or denied and no further rules are examined. A rule is matched when the signer matches the identity field, the name matches the name field, and the type is specified in the type field.

The identity field specifies a name or a wildcard name. The nametype field has 4 values: name, subdomain, and self

| name | Matches when the updated name is the same as the name in the name field |
| subdomain | Matches when the updated name is a subdomain of the name field (which includes the name itself). |
| wildcard | Matches when the updated name is a valid expansion of the wildcard name in the name field |
| self | Matches when the updated name is the same as the message signer. The name field is ignored |

If no types are specified, the rule matches all types except SIG, NS, SOA, and NXT. Types may be specified by name, including "ANY" (ANY matches all types except NXT, which can never be updated.

# 6.3. Zone File

# 6.3.1. Types of Resource Records and When to Use Them

This section, largely borrowed from RFC 1034, describes the concept of a Resource Record (RR) and explains when each is used. Since the publication of RFC 1034, several new RRs have been identified and implemented in the DNS. These are also included.

# 6.3.1.1. Resource Records

A domain name identifies a node. Each node has a set of resource information, which may be empty. The