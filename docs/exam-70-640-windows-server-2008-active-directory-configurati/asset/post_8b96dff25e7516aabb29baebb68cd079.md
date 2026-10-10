
![](img/a8ee53dbf1310726255b6fbb9f296fb2_48_0.png)

> **TAKE NOTE**
>
> The first domain created within an Active Directory forest is called the **forest root domain**.

## Working with Organizational Units

An Active Directory domain can contain one or more *organizational units (OUs)* that can further subdivide users and resources. An OU is a container that represents a logical grouping of resources that have similar security or administrative guidelines.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_48_1.png)

> **REF**
>
> In addition to security administration and delegation, OUs also can be used to apply and manage Group Policy Objects (GPOs). For more information about GPOs, refer to Lessons 7 and 10.

Like the parent–child relationships possible with domains, OUs can be nested in a hierarchical fashion in which a parent OU can contain one or more child OUs. Each child OU can be a parent to child OUs of its own. However, although it is possible to create a nested OU structure containing a number of parent–child relationships, you must consider that these subsequent relationships can make the administration of OUs difficult if they are nested too deeply.

An Active Directory OU structure can reflect the logical structure of the organization by modeling the company's organizational chart, depicting employees and their respective departments, or by organizing users according to their resource needs. For example, all users who have similar resource needs can be placed in an OU for ease of management if this best supports the business needs of the organization. By default, security settings that are applied to an OU will be inherited by all child objects of the container. This simplifies management by allowing you to apply a security setting once at the OU level rather than applying a setting individually to dozens or hundreds of user or computer objects contained within that OU. Administration of an OU also can be delegated to a departmental supervisor or manager and thus can allow that person to manage day-to-day resource access or more mundane tasks, such as resetting passwords. This is referred to as *delegation of control*. Each container or OU can be created with custom security guidelines in mind, allowing detailed administrative control.

OUs can contain the following objects:

-   Users
-   Groups
-   Contacts
-   Printers
-   Shared folders
-   Computers
-   OUs
-   InetOrgPerson

Beginning in Windows Server 2003, Active Directory also includes a fourth partition type called an *application partition*. Application partitions provide fine control. Administrators can direct where information is replicated to a domain or forest. This results in greater flexibility and better control over replication performance. For example, the DomainDNSZones application partition will replicate information to every DNS server within a single domain; the ForestDNSZones application partition will replicate data to every DNS server in a forest.

## Understanding the Schema

The Active Directory schema defines what different types of objects look like within Active Directory. What is a user? What properties does a group have? Active Directory comes with a prepopulated base schema, and it can be modified or extended to meet the needs of custom applications.

Every resource in Active Directory is represented as an *object*, and each object has a set of *attributes* that are associated with it. In Active Directory, each object is defined within the Active Directory *schema*. The schema is a master database that contains definitions of all objects in the Active Directory—in a way, it defines what Active Directory *is*. The schema has two components: *object classes* and *attributes*. Each object that is represented in Active Directory—for example, the user John and the printer Laserprinter—is an instance of the user and printer object classes, respectively.

Each object class in the schema is further defined according to a list of attributes that make the object class unique within the database. The list of attributes is defined only once in the schema, but the same attribute can be associated with more than one object class. Some attributes are *required* attributes that are necessary for the object to be created, such as a user account logon name. Other *optional* attributes, such as street address and phone number, provide additional details that can be published for user and administrative purposes.

When Active Directory is installed, a number of object classes are created automatically. Some of these object classes include:

-   Users
-   Groups
-   Computers
-   Domain controllers
-   Printers

All object classes have a common set of attributes that help to uniquely identify each object within the database. Some of these common attributes are as follows:

-   **Unique name.** This name identifies the object in the database. A unique name is given to the object upon its creation and includes references to its location within the directory database. This will be explained later in this lesson.
-   **Globally unique identifier (GUID).** The GUID is a 128-bit hexadecimal number that is assigned to every object in the Active Directory forest upon its creation. This number does not change, even when the object itself is renamed. The number is not used again, even if an object is deleted and recreated with the same display name.
-   **Required object attributes.** These attributes are required for the object to function. In particular, the user account must have a unique name and a password entered upon creation.
-   **Optional object attributes.** These attributes add information that is not critical to the object in terms of functionality. This type of information is “nice to know” as opposed to “need to know.” An example of an optional object attribute would be a phone number or street address for a user account.

As you will see, the schema can be modified to include additional objects and attributes when necessary. Each object in the schema is protected by access control lists (ACLs) so that only authorized administrators can access and modify the schema. ACLs are implemented by the administrator and used by the directory to keep track of which users and groups have permission to access specific objects and to what degree they can use or modify them.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_49_0.png)

> The Active Directory schema is managed using the *Active Directory Schema* tool. Because modifying the schema is a sensitive operation, this tool does not exist by default in the Administrative Tools folder. The snap-in must be added manually. For more information about adding this tool, refer to Lesson 2.

## Creating Active Directory Sites and Subnets

> *A site* is defined as one or more IP subnets that are connected by fast links. In most circumstances, all computers that are connected via a single LAN will constitute a single site. Within Active Directory, sites are used to optimize the replication of Active Directory information across small or large geographic areas.

All domain controllers within the same site will use intrasite replication to replicate information as changes are made to Active Directory, whereas intersite replication takes place at regularly scheduled intervals that are defined by an administrator. An internal Active Directory process known as the *Knowledge Consistency Checker* (*KCC*) automatically creates and maintains the replication topology. The KCC operates based on the information provided by an administrator in the Active Directory Sites and Services snap-in, which is located in the Administrative Tools folder on a domain controller or an administrative workstation that has had the Administrative Tools installed.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_49_1.png)

> For more information about the *KCC*, replication, and the use of the Active Directory Sites and Services snap-in, refer to *Lesson 3*.
