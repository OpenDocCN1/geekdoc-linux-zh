# Declarations

You might want to group different clients for several reasons, such as organizational requirements, network layout, and administrative domains. To assist with grouping these, you can make use of certain declarations. We discuss this and other declarations in the following sections.

Individually listing parameters and declarations for each host and again can make the configuration file difficult to manage. The group declaration allows you to apply a set of parameters and declarations to a list of clients, shared networks, and subnets. The syntax for the group declaration is as follows:

```
group label
[parameters]
[subdeclarations]
```

Here, label is a user-defined name for identifying the group. The parameters block contains a list of parameters that are applied to the group. The subdeclarations are used in case a further level of granularity to describe any additional clients that might be a member of the current declaration.

Ignore the parameters field for now. It will be covered in the upcoming section “Parameters."

host declaration is used to apply a set of parameters and declarations to a particular host in addition to the parameters specified for the group. This is commonly used for fixed address booting or for the BOOTP clients. The syntax for a host declaration is as follows:

```
host label
[parameters]
[subdeclarations]
```

Here, label is the user-defined name for the host group. The parameters and subdeclarations are described in the group declaration.

shared-network declaration groups a set of addresses of members of the same physical network. This allows parameters and declarations to be grouped for administrative purposes. Here’s the syntax:

```
shared-network label
[parameters]
[subdeclarations]
```

Here, label is the user-defined name for the shared network. The parameters and subdeclarations are described in the group declaration.