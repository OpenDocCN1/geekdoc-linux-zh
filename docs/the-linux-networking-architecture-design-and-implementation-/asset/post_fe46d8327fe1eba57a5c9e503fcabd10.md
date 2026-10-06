
```c
struct ip_conntrack_tuple tuple;
struct ip_conntrack_tuple mask;
/* Helper function: returns verdict */
unsigned int (*help)(struct ip_conntrack *ct,
struct ip_nat_info *info,
enum ip_conntrack_info ctinfo,
unsigned int hooknum,
struct sk_buff **pskb);
};

const char *name;
```

help is a pointer to the main function of the helper module, which is invoked by do_bindings(), as was mentioned previously.

# Extending the Linux Network Architecture Functionality—KIDS

This chapter deals with the introduction of new, dynamically extendable functionalities in the Linux network architecture or in the Linux kernel. We will first show the usual approach to manage dynamically extendable functionalities and the operations generally involved in this approach.

Subsequently, we will use Linux KIDS, the implementation of a construction system to support network services, to show how a dynamically extendable functionality can be managed. Another interesting aspect of Linux KIDS is how its object-oriented concept is implemented in the Linux kernel, considering that the Linux kernel was not designed with object orientation in mind.

In addition, we will explain how the KIDS components can be embedded into the processes of protocol instances over existing interfaces, which means that you can use the functionality of Linux KIDS without having to change the kernel source code. Finally, this chapter describes how you can use a character-oriented device to configure the KIDS construction system, allowing you to easily configure this functionality in the kernel.

## 22.1 MANAGING DYNAMICALLY EXTENDABLE FUNCTIONILITIES

The Linux network architecture is continually extended by new functions and protocol instances. In most cases, such an extension can be dynamic (i.e., at runtime), as we saw in earlier chapters: network-layer protocols (Section 6.3), transport-layer protocols (Section 14.2.5), and packet filters (Section 19.3).

All we need to implement such a dynamic extensibility is an appropriate interface and structures that manage the registered functionality. Functions like register_functionality() and unregister_functionality() can be used to register new functionalities with the kernel or remove existing functionalities.

## 22.1 Managing Dynamically Extendable Functionalities

These registering and unregister functions execute all initialization and cleanup steps required. For example, when removing a functionality, we have to ensure that it is longer used in any other location of the kernel. This has to use a reference counter (use counter) and check this counter (use_counter == 0?) beforeunregistering a functionality.

The following operations are some of those normally executed in the registration function of interface and undone, accordingly:

- storing the new functionality of its management structure in a list, hash table, or another data structure;
- reserving memory for the required data structures and procuring other resources (IRQ, DMA, timer, etc.);
- incrementing reference counters;
- creating entries in the proc directory;
- using printk() to output status messages.

A new functionality (e.g., a new network-layer protocol or a network device) normally takes many parameters. It would be difficult to pass all of these parameters individually in the registration function, because they are required while the functionality is being used, which is normally outside the registration function. For a reason, to structure to manage the functionality this structure can be registered in a list, hash table, or similar management structures. This method ensures that we can access these functionalities and their parameters after the registration. Earlier chapters introduced a large number of such management structures, including the net_device structure for network devices and the packet_type structure for network-layer protocols.

Such a management structure is filled with the parameters required before it is registered. Subsequently, a pointer to this management structure is passed to the registration function. The elements of these management structures assume two tasks:

Configuration data is set before a functionality is registered and as (configuration) parameter within the structure. In the packet_type structure (Chapter 6), for example, these parameters include the type and func variables. Runtime variables are not explicitly set before a functionality is registered. They are needed later when the functionality is used (e.g., next to list structures, or a counter to count references).

After a registration, of course, we can also use configuration variables as runtime variables, if the initial value is no longer needed.

After this overview of the principles of how to manage functionalities dynamically, the sections following discuss how the KIDS framework is implemented in the Linux kernel 2.4 (Linux KIDS). This framework relies heavily on the concept of dynamically extendable functionalities, as shown in our Linux KIDS example further below. Another interesting point is that the components and their instances are based on the object-oriented concept, and this approach could probably be for other software projects in the Linux kernel. The next section begins with an intro-duction of its basics to better understand how the KIDS construction system works.

## 22.2 STRUCTURE OF THE KIDS CONSTRUCTION SYSTEM

KIDS stands for Karlsruhe Implementation architecture of Differentiated Services and was developed for the design, evaluation, and use of quality-of-service (QoS) meisms in networks [Wehr01b]. KIDS is an abstract model describing the structure and interaction of quality-of-service mechanisms, and it allows you to define individual QoS behavior in a flexible way. The KIDS framework was implemented on various platforms, including Linux (kernel Version 2.4) and OMeT-- simulation tool. Although Linux already supports some QoS features (Chapter 18), KIDS introduces important benefits, as we will see in the future course of this chapter. The next two sections will introduce the general structure of the KIDS framework; however, we will leave out a few details to keep things short—[Wehr01a] for details.

### 22.2.1 Elementary QoS Components

KIDS was designed to create a flexible, extendable, and modular framework for imple-menting individual QoS mechanisms. It is based on the use of components that imple-ment the elementary QoS mechanisms, and so it is easy to combine them to more complex QoS mechanisms. Simple combination of components and ensuring all poten-tial degrees of freedom and easy extendability were the most important factors in the design of the KIDS framework.

KIDS can be thought of as a construction kit, similarly to the popular Lego sys-tem consisting of components that have different interfaces. Components with similar interfaces can be connected (almost arbitrarily) to form complex constructions (in this case QoS mechanisms).

We can distinguish two different interfaces in the components of the KIDS framework (as seen in Figure 22–1):

![](img/5a25b942ec3329b8799f2b5f0de564f6_451_0.png)

FIGURE 22–1
Interactions at the interfaces between two components.

## 22.2 Structure of the KIDS Construction System

At a packet interface (O), a component uses packet output X to pass a data packet it received at its input to the successor component, B. By convention, a KIDS component has but a single input.

At a message interface (O), component uses message output X to pass a message to component B, requesting the letter for the packet.

Using these two interface types, we can distinguish five component classes, as shown in Figure 22–2. Each QoS mechanism can be assigned to one of these classes:

- Examples: Token Bucket, Shaper, Marker, Dropper, Classifier, Random Early Detection (RED).
- Queue components (QUEUE) are data structures used by components to enqueue or dequeue packets.
- Examples: FIFO Queue, Enqueue-Deadline-First-Queue.
- Enqueuing components (ENQ_BHVR) enqueue packets in queues based on special methods, which is the reason why they have no outputs.
- Examples: Head-Enqueue, Tail-Enqueue, EDF-Enqueue.
- Dequeuing components (DEG_BHVR) dequeue packets from a queue based on a special method. They receive a dequeue request on their message input and subsequently try to dequeue a packet from the queue. If successful, the packet is transported from the packet output; otherwise, a negative message is returned.
- Examples: Head-Dequeue, Tail-Dequeue.
- Strategic components (DEG_DISC) implement special strategies that can be combined in a flexible way to serve queues. This means that they decide on the route for dequeue requests to dequeue components, which eventually serve the queue.
- Examples: Priority Queuing, Weighted Fair Queuing, Round Robin.

![](img/5a25b942ec3329b8799f2b5f0de564f6_452_0.png)

Figure 22–2
Five different KIDS component classes.
