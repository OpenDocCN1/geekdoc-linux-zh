# 10.3 Namespace: Keyspace

# Intent

Provide namespaces for referring to protocols, structures, or other entities in a program.

# Motivation

A typical sensor network program needs namespaces for the various entities it manages, such as protocols, data types, or structure instances. Limited resources mean names are usually stored as small integer keys.

For data types representing internal program structures, each instance must have a unique name, but as they are only relevant to a single mote, the names can be chosen freely. These local namespaces are usually dense, for efficiency. The Service Instance pattern (Section 10.2) uses a local namespace to identify instances. In contrast, communication requires a shared, global namespace: two notes/applications must agree on an element's name. As a mote may only use a few elements, global namespaces are typically sparse. The Dispatcher pattern (Section 10.1) uses a global namespace to select operations.

The Keyspace patterns provide solutions to these problems. Using these patterns, programs can refer to elements using identifiers optimized for their particular use. Components using the Keyspace patterns often take advantage of a parameterized interface, in which the parameter is an element in a Keyspace. Local Keyspaces are designed for referring to local data structures (e.g. arrays) and are generated with unique; Global Keyspaces are designed for communication and use global constants (normally defined using enum).

The AM identifiers used to distinguish message types form a Global Keyspace. ActiveMessageC uses these AM identifiers in conjunction with a Dispatcher to execute the appropriate message handlers found in other components. Local Keyspaces have other uses than identifying clients in the Service Instance pattern: the Maté virtual machine uses a Local Keyspace to identify locks corresponding to resources used by Maté programs. These lock identifiers are allocated with unique as the Maté virtual machine can be compiled with varying sets of resources.

# Applicable when

+   - A program must keep track of a set of elements or data types.
+   - The set is known and fixed at compile-time.

# Sample code

The AM identifiers for the SoundLocalizer application (Chapter 13) are defined as global constants:

```
enum {
  AM_COORDINATION_MSG = 101,
  AM_DETECTION_MSG = 102
};
```