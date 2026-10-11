Within the rule, you specify the attributes you want entries matched on between systems. For example, you could specify that entries be matched between systems on the given name and surname attributes.

When an Add Object event is detected, the matching rule is invoked and a connection is made between the data source and destination systems. The matching rule then attempts to find an *existing entry* in the destination system that matches the new entry based on the given name and surname attributes.

If a single match is found in the destination system, an *association* is established between the two entries. Essentially, the new entry in the source system is said to be the same as the entry found in the destination system.

To understand associations, you need to understand that the databases synchronized by DirXML each use different attributes to function as unique identifiers for database entries. No two entries in the DirXML system can have attributes that share the same values.

In one system, it might be the globally unique ID (GUID) attribute. In another system, it could be the employee number attribute.

When DirXML is installed, the eDirectory schema is extended, and each object in the tree has an *association* attribute added to it. If the matching rule identifies an association between two entries, the association attribute of the eDirectory object is populated with the ID of the correlating entry in the other system. This is shown in Figure 7.5.

![](bbox=[0.05, 0.61, 0.87, 0.74])

If multiple matches are found based on the matching rule criteria, DirXML will discard the event. If no match is found, the Add Object event is propagated on to the next rule.

Besides the matching rules are a handful of others to be aware of:

+   * **Creation rules**—*Creation rules also exist on both the publisher and the subscriber channels. The creation rule is applied after the matching rule has been applied.