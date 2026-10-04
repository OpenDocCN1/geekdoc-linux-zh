# Securing Active Directory • Chapter 6

Compatible Access” (it also exists in a native mode, but does not have any members by default), which contains the “Everyone” Security ID. Members of this group have the access permissions shown in Table 6.2.

# Table 6.2 Access Permissions for Everyone

| Object | Permissions Granted | Permission Applied to |
| --- | --- | --- |
| Catalog root | List contents | This object and its subobjects |
| User objects | List contents, read properties, read permissions | User objects |
| Group objects | List contents, read properties, read permissions | Group objects |

These permissions allow in certain cases browsing of the information in Active Directory to the much bigger extent it is supposed to, even for anonymous users. You will see the examples of how this situation can be exploited in the later section “Conducting Attacks on Active Directory.”

# Schema

The schema is the list of the types of objects that can be created within an Active Directory forest, and the attributes that any object can have. Objects are user accounts, computer accounts, group accounts, and network resources. Attributes are descriptive values for the objects. For example, a person named Ulysses assuming the naming convention was first concatenated with the last name. The first name attribute “USER” would be “ULYSSES,” and the last name attribute of “USER” would be “SER”.

The schema can be extended to include new objects and attributes. This extensibility can enable an application or corporation to customize Active Directory for its uses. The possibilities are endless. If an application for Time and Billing extended the Active Directory, it might add attributes to user objects for a billing rate. Furthermore, the database itself could be represented in Active Directory by a time and billing object. Then, the users and groups can be granted or denied access to the database.

Even if you do not plan to extend the schema, you may find that it is necessary to an application’s requirements. For example, Exchange 2000 requires that the schema extended to include the objects and attributes necessary for Active Directory to act as a directory service for a messaging platform. In addition, you may find that there are attributes you would like to have included

![](bbox=[0.708, 0.946, 0.923, 0.966])