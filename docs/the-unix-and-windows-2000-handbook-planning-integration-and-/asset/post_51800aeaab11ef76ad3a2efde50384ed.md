
![](img/415c89a1ede71e11e5040a0038b6916c_299_0.png)

# Figure 7.14 Active Directory Users and Computers MMC snap-in.

from any tree or domain in the forest, and are replicated outside of their parent domain. Universal groups appear in the global catalog, described later in this chapter. Global groups may only contain users and groups from the same domain, but are listed in the global catalog. The membership list of a global group is not published outside the domain. Last, but not least, domain local groups may contain users and groups from multiple domains, but can only be used in ACLs in the same domain. Domain local groups are not replicated outside of the domain and are not published in the global catalog. Windows 2000 also includes many built-in groups, as shown in Figure 7.15.

Machine accounts are created when any workstation joins a Windows 2000 domain. While this is very similar to the machine accounts created in Windows NT 4.0, Windows 2000 can contain machine accounts for tracking purposes, even if a machine does not participate in domain security.

Attributes Attributes are the individual pieces of information that describe the objects contained in object classes. A user object class requires attributes that are distinctly different from the attributes required by a printer object class or an application object class.

## Editing the Schema

The attributes attached to an object class can be viewed and edited using the Active Directory Schema MMC snap-in shown

![](img/415c89a1ede71e11e5040a0038b6916c_302_0.png)

## ACTIVE DIRECTORY FEATURES

Active Directory provides several new features over the traditional Windows NT domain model. Among the new features are integration with the domain name system, multi-master domain controller replication, enhanced domain security (including true parent-child relationships), a global catalog for quick searching, and the use of the industry standard Lightweight Directory Access Protocol (LDAP) for directory access. This section will provide a basic explanation of these features, which will help you to understand AD and effectively use it within your organization.

### DNS Integration

Another important feature of AD is its integration with the Domain Name System (DNS). In previous versions of Windows, WINS or some other Net-BIOS naming service was used to resolve Windows computer names to IP addresses. Previous versions of Windows also used WINS to locate Windows NT domain controllers on the network. Anyone who has managed a Windows NT network knows that WINS can be very tricky to bring on-line and that it doesn't always work properly. Active Directory uses the industry-standard DNS for all name resolution (WINS can be used for compatibility with older client systems), thus eliminating the need for WINS servers.

In the AD world, DNS is used for resolving Windows machine names to IP addresses, as well as for locating domain controllers and network services. Now, anyone who knows about DNS also knows that most current DNS servers do not have provisions for entries describing Windows domain controllers and network services. Of course, the DNS server packaged with Windows 2000 provides the necessary additions to support Dynamic Update (RFC 2136) and Service Resource Records (SRV RRs). DNS Dynamic Update allows servers and clients to publish DNS updates directly to the DNS server, without administrative intervention. Service Resource Records allow client workstations to locate network services (such as LDAP, which is used by AD and is discussed later in this chapter) by querying DNS for a service.protocol.domain record. For instance, to locate an AD server on our network, a DNS client would query DNS for ldap.tcp.ece.gatech.edu, which should point to the closest LDAP server on the network. Fortunately, for those of us who prefer a UNIX-based DNS server, the latest version of the popular BIND server also supports DNS Dynamic Update and Service Resource Records. This allows both UNIX and Windows 2000 DNS servers to provide fully functional name resolution services for your UNIX and Windows 2000 systems.

> Many of you are probably not running the latest version of BIND. If you wish to use a UNIX-based DNS system for Windows 2000, you must upgrade to the newer version of BIND to support Service Resource Records.

### Domain Controllers and Partitioning

What you currently know about Windows NT domain controllers is about to drastically change. Currently, a Windows NT domain consists of a single Primary Domain Controller (PDC), one or more Backup Domain Controllers (BDCs), and member servers and workstations. The days of PDCs and BDCs are gone with the introduction of Active Directory.

In the AD world, all domain controllers are created equal; that is, there is no longer a master-slave relationship between domain controllers. Each domain controller in an AD domain can service logon requests, receive updates, and replicate those updates to other domain controllers in the domain. In large networks, there can be literally hundreds of thousands of objects in the AD. However, it doesn't make much sense for every domain controller to manage the entire AD database individually. Instead, you can partition your domain controllers such that each one manages a different section of the database. Not only does this reduce the load on any single domain controller, it also will allow you to logically assign "tasks" to each domain controller. While this is not necessary in small domains, the benefits become clear when we scale to domains that contain several thousand or even over a million objects.
