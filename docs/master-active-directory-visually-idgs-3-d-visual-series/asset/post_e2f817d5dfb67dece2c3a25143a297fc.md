
# CONFIGURING TRUSTS

Trust relationships allow two domains to share information. Windows 2000 makes trust relationships easier by implementing transitive trusts through the Kerberos security protocol. Windows 2000 domain controllers in the same domain, domain tree, or domain forest automatically trust each other through transitive trusts that are configured automatically. You can also establish trust relationships with other domains that are not Windows 2000 Active Directory domains. This is performed by manually establishing the nontransitive trust on the Trusts tab of the domain properties. You must also manually establish a trust relationship for two Active Directory forests that want to communicate with each other. After you configure trust relationships, you can access the trust's properties sheets. You can use the properties sheets to specify service principal name (SPN) suffixes, if desired. Servers identify themselves by using an SPN. Normally, this is the full DNS name of the server, but you can create different SPN suffixes for externally trusted domains so that the server does not have to reveal its full DNS name. This is a security feature of Windows 2000.

![](img/763d5ae436311371600c0952a3da9094_383_0.png)

![](img/763d5ae436311371600c0952a3da9094_383_1.png)

- 1. Select the domain you want to administer, and then choose Action > Properties.
- 2. To create a trust relationship, click Add to enter domains that trust and are trusted by your domain. The Added Trusted Domain dialog box appears.
- 3. Type the trusted domain's name.
- 4. Type the password used to establish the trust relationship.
- 5. Retype the password to confirm.
- 6. Click OK.

# TIPS

## What is a transitive trust?

A transitive trust is a feature of the Kerberos security protocol built into Windows 2000. A transitive trust is two-way between two domains. Also, Kerberos trusts are transitive—this means that a domain can automatically trust another domain without a direct trust relationship. For example, if Domain1 trusts Domain2 and Domain2 trusts Domain3, then Domain1 automatically trusts Domain3. Transitive trusts are automatically created for Active Directory domain controllers in a tree or forest. This is a new way of establishing trust relationships in Windows 2000; Windows NT did not allow any type of transitive trusts.

## What is a nontransitive trust?

Nontransitive trusts are trust relationships that do not support the Kerberos security protocol. Administrators on each side of the trust relationship must configure a nontransitive trust. If DomainA trusts DomainB, this doesn't mean that DomainB trusts DomainA as it does in a transitive trust relationship. Nontransitive trusts are also static. In other words, if DomainA trusts DomainB and DomainB trusts DomainC, DomainA does not automatically trust DomainC.

![](img/763d5ae436311371600c0952a3da9094_384_0.png)

- 1. On the Trusts tab, select a trust relationship and click Edit to see the properties page. The properties sheet appears. The General tab gives you information about the trust relationship.
- 5. Click the SPN Suffixes tab.
- 6. Click Add.
- 7. Enter trusted SPN suffixes as desired.

# ASSIGNING A DOMAIN MANAGER

As with other Active Directory components and services, you can assign a manager to the domain. A *manager* is the person who can "manage" the domain properties. This feature enables you to distribute the administrative duties and roles to other Active Directory users as necessary.

As with any Active Directory administration, you should be careful who you choose to be manager of the domain. That person should have the skills necessary to administer the domain, and that person must act responsibly with any configuration changes. Remember that a manager can change the domain mode and configure trust relationships. Both of these actions can cause severe problems in your domain without proper planning, and you only want highly skilled administrators making these kinds of changes. So, the key advice is to use a manager if needed, but wisely assign the role.

![](img/763d5ae436311371600c0952a3da9094_385_0.png)

- 1. Select the domain where you want to assign a manager, and then choose **Action → Properties**.
- 2. Click the **Managed By** tab.
- 3. Click **Change**.

![](img/763d5ae436311371600c0952a3da9094_385_1.png)

## What qualifications should I look for in a potential manager?

Anyone that is assigned a managerial role in the Active Directory should meet these qualifications:
- The manager should have solid technical skills concerning the Active Directory.
- The manager should be aware of domain problems, issues, and upcoming changes.
- The manager should have a direct reporting line so that he or she can gain correct information before undertaking any configuration changes.
- The manager should be reliable and responsible.

## Can I change the domain manager?

Yes. You can change the manager of the domain, or the manager of any Active Directory object at any time by accessing the Managed By tab and clicking the Change button. You can then select a new manager from the Active Directory. Of course, changes in managers should always be carefully planned to ensure that you are assigning managerial roles to acceptable users or system administrators.

![](img/763d5ae436311371600c0952a3da9094_386_0.png)

- 4. Select the user that you want to become the domain manager. The selected name appears in the Name dialog box.
- 5. Click OK.

![](img/763d5ae436311371600c0952a3da9094_386_1.png)

- The new manager now appears on the Managed By tab.
- 6. Click OK to close the Properties sheets.

# SECTION VII

# 22) MANAGING ACTIVE DIRECTORY SITES

- Introduction to Active Directory Sites 366
- Using the Active Directory Sites and Services Snap-in 368
- Administering the Sites Container 372
- Creating a New Site 378
- Delegating Control of the Sites Container 380

# 23) CONFIGURING ACTIVE DIRECTORY SITE COMMUNICATIONS

- Examining Site Properties 384
- Configuring Site Settings 388
- Creating Site Links 396
- Configuring Site Links 400
- Creating and Configuring Subnets 402

![](img/763d5ae436311371600c0952a3da9094_388_0.png)

# INTRODUCTION TO ACTIVE DIRECTORY SITES

The Active Directory Sites and Services MMC snap-in is used to manage both Active Directory sites as well as services pertaining to sites. Before you take a look at the configuration of sites in this chapter, this section examines the function of sites and related technologies.

offices in New York, Dallas, and Phoenix, each city location can be a site within the WAN.

## What is a site?

A Windows 2000 site is a physical grouping of computers and/or domains. A site organizes computers, domain controllers, and even domains in a particular location. Typically, sites are used in WAN environments in which a company has offices in several geographic locations. For example, if Wellington Consultants has

## What is the difference between a site and a domain?

The terms site and domain are often confused. A domain is a logical grouping of computers; a site is a physical grouping of computers. You can have multiple domains within a single site. Domains organize users and computers within a site; a site is the physical location of those users, computers, and domains. For example, within the New York site of Wellington Consultants, you could have two domains: one for Accounting and one for Marketing.

![](img/763d5ae436311371600c0952a3da9094_389_0.png)

# **Why use sites?**

Because sites are typically used to segment physical locations of the WAN, sites help control how users access services and how bandwidth is conserved. A site can keep user access within its own subnet, unless a particular service becomes unavailable.

First, a subnet helps user authentication. Because the Active Directory uses multimaster replication, any Windows 2000 domain controller on the network can authenticate any user. This can present a problem with WAN bandwidth. The site keeps user authentication within the subnet so that the domain controllers in that subnet can first authenticate the user before the request is sent to other sites. This keeps the traffic localized on the subnet.

Next, you can use site links to control how the Active Directory replicates information among domain controllers at different sites. This feature helps you control bandwidth usage and fault tolerance among the sites. Along with the site links, you can also specify a bridgehead server. A bridgehead server is a server that is specified to send and receive intersite replication data. By default, all domain controllers replicate information to each other. The bridgehead server takes care of this process because it is dedicated to intersite replication.

Aside from authentication and replication, the sites also control user service requests to domain controllers. As with authentication, the service requests are directed to the domain controllers within the site instead of domain controllers in other sites.

![](img/763d5ae436311371600c0952a3da9094_390_0.png)

![](img/763d5ae436311371600c0952a3da9094_390_1.png)
