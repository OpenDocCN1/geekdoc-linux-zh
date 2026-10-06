
# Working with LDAP in SUSE

Back in the day, the only way to centrally manage your users and services was to use Network Information System (NIS). NIS was an endeavor by Sun to help administrators manage their users without having to create accounts locally on all machines.

NIS is capable of maintaining user account information, groups, services, hosts, and many more pieces of information that, historically, needed to be managed on a local level.

NIS was great for what it did at the time, but it had a few shortcomings; one problem, in particular, was it wasn't great at dealing with very large amounts of data. We don't mean the physical size of the data, but the management of that data. NIS uses flat files as input to the NIS database, which does not bode well in large infrastructures. One other major drawback of NIS was that could not store any other information apart from account and systems data.

One way around this management problem is to use a tree to organize data in a manageable fashion. This is where LDAP comes to the rescue.

Lightweight Directory Access Protocol (LDAP) organizes data in a hierarchical structure, allowing you to organize information based on departments, or any other distinguishing method.

When introducing people to LDAP, we have always found that it is not an easy concept to explain because it is not easily explained compared to any existing technology. In this chapter, we give you an overview of what LDAP is, its uses, how to populate an LDAP server with information, and also a scenario that is common to the use of LDAP; including configuration.

# CHAPTER 25

# In This Chapter

- What is LDAP?
- Implementing LDAP
- Integrating Linux with LDAP

# What Is LDAP?

LDAP is not a specific server. Much in the same way that Domain Name System (DNS) and Simple Mail Transport Protocol (SMTP) are conceptual protocols, LDAP describes the organization of data, access to the data, and the protocol used to access an LDAP server.

The Linux LDAP implementation is the extremely popular OpenLDAP server. It has been around for a very long time and uses the LDAP specification as a base to implement new features.

LDAP is a part of many organizations although many people in those organizations aren't aware of its use. The Active Directory service from Microsoft is heavily based on the LDAP protocol, as is Novell's eDirectory implementation.

The main distinguishing factor of LDAP is in the way it stores its information. All data in an LDAP database is stored in a tree. LDAP is an inverse tree in the same way that your filesystem is. At the top of the LDAP tree, you have the base object, usually the organization. Below this, you then have objects that are part of the LDAP tree, or you can have a further split using subtrees.

Figure 25-1 puts this structure into a diagram.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_680_0.png)

Figure 25-1: Conceptual overview of LDAP

When thinking about LDAP, try to think not on a technology level, but on an organizational level. LDAP design should follow the organization of what you are storing data about. For our example, we will take the organization of a fictional company called Acme Technology. Acme, like many organizations, has departments that deal with certain parts of the business (Sales, Marketing, HR, IT, the Board, and so on), and we will model this in our LDAP server.

We have taken the IT department and expanded it slightly to include job title and some people in the organization. You may be thinking that this looks like a standard organizational chart that you see when you start a company, and this is how you view it. All the people in the organization belong to a department, which belongs to the organization, and this methodology is how you see LDAP. The tree structure itself lends well to organizational data, whether it is just for address book or user accounts.

# LDAP Objects

LDAP uses objects to store data. Take the user object as an example. You can store a lot of information about a user: first and last name, location, telephone, pager, mobile. LDAP uses classes to define what information can be stored about that object, commonly known as attributes. LDAP is very particular about information you store in the LDAP server because it needs to maintain the integrity of all data. To do this, an object is specifically defined that must include certain data and will include nothing else. For example, the employee Jane Doe; the record can contain her first, middle, and last name; employee ID; Social Security number; telephone number; email address; date of birth; and her location (is not exhaustive). The other hand, her record may contain information about her car (if she has one), pager number (if she has one), and home number. Any other data will not be allowed because the object is strictly defined. Object definitions are in the LDAP schema, which we talk about later.

# The Hierarchy

You know LDAP is a hierarchical database, but you may not be aware of all the benefits of this. Imagine on your filesystem, you have a home directory for a user called Justin /home/justin. Inside this directory, you have a subdirectory Documents with a further subdirectory of Finances. Another user, Roger, has a home directory of /home/roger. Roger also stores information about his finances in Documents directory. It happens that Roger and Justin have the same filename, these do not impact each other because their location is different throughout the filesystem. LDAP works the same way. If a person called John Doe joins as HR assistant and another John Doe (a popular name) joins as as architect, their locations in the tree mean that their information is uniquely identified by the path to that data. Figure 25-2 shows another diagram of Acme with LDAP to explain how LDAP uses the tree design.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_682_0.png)

**Figure 25-2**: Acme organization in LDAP

We have replaced the organizational chart with an LDAP structure. Reading back from Jane Doe, which is like from the finances file, you can uniquely identify this person in the organization. In the case of Jane Doe, her unique entry is cn="Jane Doe", ou=Helpdesk, ou=IT, o=Acme, c=UK.

Notice the quotes around Jane Doe in the previous entry. This is to make sure the space is included in the cn for Jane. From this information, you see that Jane Doe is in the organization Acme (UK), the department of IT, and the subdepartment Helpdesk. The person Jane Doe is unique in the organization, working on the Helpdesk, and is unique in the LDAP directory. This unique identifier is called the Distinguished Name (dn), and we will refer to it for the rest of the chapter.

This is a quick introduction to how LDAP stores data, and throughout the rest of the chapter, you will learn by example using LDAP in the Acme organization, taking the organizational chart as a basis for its design.

Designing an LDAP directory is something that has to be done correctly. If you have an up-to-date organizational chart that effectively represents your organization, your life will be a bit easier.

# Implementing the LDAP Server

When you have installed the Open LDAP server using YaST, you need to do some initial configuration. The LDAP server is configured in the file /etc/openldap/slapd.conf and is heavily commented. The two very important parts you need to configure before even starting to populate the server are the basedn and the administrator account.

# Configuring the Administrator

The basedn is the very top of the LDAP tree. In the base of Acme, the basedn will be o=Acme, c=UK. The o component means Organization, the c component refers to country. With everything in LDAP, there are strict rules on naming the basedn. Most common elements are the c- and dc- but the general domain component (dc) is used to refer to the fully qualified domain name (FQDN) of the organization. In the case of Acme, you could use a basedn of dc=Acme,dc=uk. However, as we are designing the LDAP structure from an organizational chart, we will use the organizational terms. To edit the LDAP configuration files, you must reboot. When you have set the username and password for the administrator account, you can use any user as long as you authenticate as the administrator when connecting to OpenLDAP.

- 1. In the slapd.conf file, find the entry for the suffix and the rootdn (the administrator user) and change it to reflect your organization.
