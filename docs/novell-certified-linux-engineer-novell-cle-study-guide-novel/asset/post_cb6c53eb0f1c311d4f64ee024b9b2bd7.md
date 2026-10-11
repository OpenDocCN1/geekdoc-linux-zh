
As the name implies, DirXML extracts data from a data source in the form of an XML document. It then uses stylesheets to transform the XML data into a format the destination system can understand. In this way, information from disparate systems can be harmonized.

Let's explore how DirXML works in more detail.

## How DirXML Works

**Test Objective Covered:**
- 2. Describe how DirXML works.

Before beginning this topic, you need to understand that DirXML is a complex product. We're going to discuss how it works at the conceptual level only. When DirXML was first released in 2000, I had the opportunity to sit in on a class taught by the software engineers who wrote the product.

The class was full of experienced network consultants. However, by the time the class ended two weeks later, we all had acquired a permanent stupefied look on our faces (accompanied by a nervous twitch). The complexity of the product and the level of detail presented in the class made our heads hurt!

Based on that experience, I will endeavor to make DirXML as easy to understand as I can in this book. Let's get started by reviewing the structure of the DirXML product and its various components.

## DirXML Components

DirXML is composed of the following elements:

- The data source
- The data destination
- The DirXML engine
- The DirXML drivers
- The subscriber channel
- The publisher channel
- The subscriber channel rules and filters
- The publisher channel rules and filters

These are shown in Figure 7.3.

![Figure 7.3](img/c7771e8540507f2b00c088c7a411b57b_300_0.png)

Let's talk about each component. The *data source* is the system (usually eDirectory) that is monitored for add, modify, and delete events. It's the authoritative data source mentioned earlier.

The *data destination* is the system to which data from the data source is being synchronized. The *DirXML engine* is the heart of DirXML. The DirXML engine itself is composed of two components: the *eDirectory interface* and the *join engine*. The eDirectory interface is used by the DirXML engine to connect with the eDirectory service on the server where eDirectory is running.

The *join engine* processes each add, modify, or delete event that comes to the DirXML engine and applies the various rules you've configured to the event. We'll talk more about rules and filters later in this chapter.

A *DirXML driver* is a product-specific driver that is used as an interface between DirXML and the product. The Starter Pack version of DirXML that comes with NNLS includes licensed drivers for Windows NT Domains, Active Directory, and eDirectory (which allows you to synchronize two eDirectory trees). It also includes evaluation drivers for PeopleSoft, Lotus Notes, and Microsoft Exchange.

DirXML drivers themselves are composed of two parts. Each driver contains an *XML interface* that is used to process XML documents going to and coming from the DirXML engine. Each driver also contains a *product-specific interface* that is used to convert information to and from the native data format of the product.

The **subscriber channel** is used to send events from the data source through the DirXML engine into the destination system. The *publisher channel* is used to receive events from the destination system through the DirXML engine and into the data source.

> **WARNING** The names of the two channels would lead one to believe that their functions are the opposite of what they really are. This is a point of considerable confusion. Remember that the subscriber channel moves data *to* the data destination and that the publisher channel moves data *from* the data destination.

Each channel contains its own set of *rules* and *filters*. The publisher and subscriber channel rules define what action is to be taken for a given event. Such items evaluated include whether “add” events should be ignored or propagated and whether “delete” events are ignored or propagated.

The publisher and subscriber channel filters are used to specify exactly what information you want synchronized. Let’s discuss rules and filters in more depth.

## DirXML Filters and Rules

Knowing how to configure rules and filters is key to effectively managing a DirXML implementation. Rules and filters help you define the direction data flows in the DirXML system and what data is replicated and what data is not.

Establishing these elements is how you define an authoritative data source. An authoritative data source is the “point of entry” into the system for network information. From this authoritative data source, data is replicated to the rest of the system.

### Configuring Authoritative Data Sources with Filters

You can filter by object class or by specific attributes within an object class. For example, you could specify that users but not groups can be synchronized from one system to the others. You could also specify that certain attributes of the user object, such as the mailing address, not be synchronized while the remaining attributes are.

To create an authoritative data source, you remove objects or attributes from the publisher channel filter while adding them to the subscriber channel filter. By doing this, you create a data flow in a single direction. This is shown in Figure 7.4.

FIGURE 7.4

Establishing authoritative data sources with DirXML filters.

![Figure 7.4](img/c7771e8540507f2b00c088c7a411b57b_302_0.png)

Once you have your filters in place, you next need to configure the various rules for each channel.

## DirXML Rules

DirXML rules define what action should be taken for a given event. The DirXML engine monitors the following types of events:

- Add Object events
- Modify Object events
- Rename Object events
- Move Object events
- Delete Object events
- Password Modification events

DirXML uses a number of different rules. Matching rules exist on both the publisher and the subscriber channels. The matching rule is the first rule applied on both channels. The matching rule is invoked whenever an Add Object event is detected.

Within the rule, you specify the attributes you want entries matched on between systems. For example, you could specify that entries be matched between systems on the given name and surname attributes.

When an Add Object event is detected, the matching rule is invoked and a connection is made between the data source and destination systems. The matching rule then attempts to find an *existing entry* in the destination system that matches the new entry based on the given name and surname attributes.

If a single match is found in the destination system, an *association* is established between the two entries. Essentially, the new entry in the source system is said to be the same as the entry found in the destination system.

To understand associations, you need to understand that the databases synchronized by DirXML each use different attributes to function as unique identifiers for database entries. No two entries in the DirXML system can have attributes that share the same values.

In one system, it might be the globally unique ID (GUID) attribute. In another system, it could be the employee number attribute.

When DirXML is installed, the eDirectory schema is extended, and each object in the tree has an *association* attribute added to it. If the matching rule identifies an association between two entries, the association attribute of the eDirectory object is populated with the ID of the correlating entry in the other system. This is shown in Figure 7.5.

![Figure 7.5](img/c7771e8540507f2b00c088c7a411b57b_303_0.png)

If multiple matches are found based on the matching rule criteria, DirXML will discard the event. If no match is found, the Add Object event is propagated on to the next rule.

Besides the matching rules are a handful of others to be aware of:

- **Creation rules**—Creation rules also exist on both the publisher and the subscriber channels. The creation rule is applied after the matching rule has been applied.
