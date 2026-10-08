# Monitoring Notes

If you intend to write your own SNMP application, the root OID of the Informix-Online Private Database MIB is **1.3.6.1.4.1.893.1.1**.

Many of the table entries in this MIB are indexed by using *applIndex* from the Network Services MIB and *rdbmsDbIndex* from the RDBMS MIB.

You can use the server mode, *onServerMode*, to determine whether the server is online, shutting down, or backing up. The MIB variable *onServerCheckpointInProgress* can give additional information about the server's activities. The Informix MIB also provides status information on all open tables, the database recovery process, and log files.

A variety of performance and resource management information is included in this MIB. For example, to determine whether your sort area is too small, you can check *onServerDiskSorts* to see how many sorts are requiring disk space.

# Using DMI and MIFs

The Desktop Management Interface (DMI) is a standard for storing and accessing management information. DMI was created by the Desktop Management Task Force (DMTF), an industry consortium focused on improving the manageability of personal computers and related products.

Management information is represented in a text file in the Management Information Format (MIF). Management information is divided by component. Each component's information consists of one or more groups, and each group has one or more attributes. If a group has multiple instantiations, then it is called a table. Each managed component must provide a separate MIF file describing its manageable attributes.

Each component has an interface to provide information to the DMI service layer. A DMI Service Provider (SP) is responsible for giving component information to the management applications that request it. Management applications communicate with the SP via DMI functions, collectively referred to as the *Procedural Management Interface*, to obtain information about a component. The interaction between these modules is shown in Figure A-4. Similar to SNMP, DMI has Get and Set commands to read and write component information.

After being queried, the SP uses additional APIs to get its information and send replies to the requesting management application. A management application can also use a list command to get information about the MIF definition itself.

The SP enables applications to register for events associated with a component. An *indication* refers to any notification by the DMI SP to an event consumer, including event notifications and notifications of changes in the SP's database, such as the addition or modification of a group in the database. The SP delivers the indication to all applications that have registered for it. The event is included in an indication data structure that is meant to look identical to a reply message to a DMI Get request.

The following list shows the required attributes associated with an indication: