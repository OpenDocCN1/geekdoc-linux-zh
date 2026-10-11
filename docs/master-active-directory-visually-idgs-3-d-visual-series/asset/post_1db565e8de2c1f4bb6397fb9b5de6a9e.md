
## ADMINISTERING THE SITES CONTAINER CONTINUED

The Advanced Security features for Active Directory objects in Windows 2000 give you greater control over the permissions you give to users and groups. This feature is particularly helpful if you want to define certain security permissions to either allow or deny access to those options.

The advanced options also enable you to configure auditing for the object as well. Auditing is configured in Windows 2000 Server, but after you configure auditing, you can choose to audit any object with the Active Directory using the advanced security options.

In most cases, you do not need to assign advanced security options to users or administrators. Under normal circumstances, the default options are all you need to give administrators the access permissions they need while not allowing Full Control permissions to unauthorized users. However, in specific cases where you need to further define a user's security permissions, the advanced features can be used and are appropriate.

![](img/763d5ae436311371600c0952a3da9094_399_0.png)

![](img/763d5ae436311371600c0952a3da9094_399_1.png)

- Click the appropriate check boxes to apply or clear permissions.

If you click the Properties tab, you can also adjust the permissions for the user or group concerning the object's properties.

- Use the Apply Onto drop-down list and Allow or Deny check boxes to assign permissions for the object's properties and that user or group.

### How does the Full Control permission apply to advanced permissions?

Remember that normal permissions, such as Read, Write, Full Control, and so on, are still in effect. The advanced permissions are simply subsets of the normal permissions. When you give a user Full Control permissions, all the advanced permissions are allowed. Likewise, if you give a user no access permission, the user is not given access in any way. The advanced permissions simply enable you to further refine any permissions you may have already given the user. In this manner, you can specify specific tasks to either permit or deny.

### Do I need to configure advanced permissions for each group?

No. Advanced permissions give you a way to finely control the permissions you give to users or groups. However, the use of advanced permissions should be incidental and not a normal part of your security plan. Under most conditions, the normal permissions you assign are all you need.

![](img/763d5ae436311371600c0952a3da9094_400_0.png)

![](img/763d5ae436311371600c0952a3da9094_400_1.png)

You can add or remove users and groups and assign them access permissions from the Access Control Settings window as well.

- Click **Add** to add users or groups and define access permissions.
- Select the user or group account from this list.
- Click **OK**.

## CREATING A NEW SITE

You create new sites by using the Active Directory Sites and Services snap-in. A site is a physical grouping of computers, normally contained within a geographic location and network subnet. A site can contain a domain or multiple domains.

When you install the Active Directory, a first site is installed by default. You can then add new sites as needed for your environment.

Each site that you create within the console should naturally reflect a physical segment of your network that has been set up to be a site. Keep in mind that each site is then connected with other sites through some kind of WAN link. You use the Sites and Services snap-in to create these sites, then you will create links between them for replication purposes.

![](img/763d5ae436311371600c0952a3da9094_401_0.png)

![](img/763d5ae436311371600c0952a3da9094_401_1.png)

### TIPS

### How should I name sites?

You can choose any naming configuration for your sites that fits your needs. The only Active Directory restriction is that site names are limited to 63 characters and cannot contain a period (.). Frequently, sites are named by their geographic location. For example, if a company has sites in Dallas, New York, and Los Angeles, the site names would reflect the cities in which those WAN sites are located.

### What is a site link?

A site link is a communication mechanism that allows one site to communicate with another. Links are typically some kind of WAN communication technology and are more expensive than a LAN connection. Active Directory site links can use Internet Protocol or Simple Mail Transport Protocol for communication.

![](img/763d5ae436311371600c0952a3da9094_402_0.png)

![](img/763d5ae436311371600c0952a3da9094_402_1.png)

- Type the name of the site.
- Select the site link object that will be associated with the site.
- You have a default IP site link if no others are configured.
- Click OK.
- Click OK.

## DELEGATING CONTROL OF THE SITES CONTAINER

You can delegate control of most Active Directory OUs or containers. When you delegate control, you allow another user or group to have control of that Active Directory object. The user or group then “owns” the object in that he or she can administer it and configure the object as needed.

As you can imagine, you should exercise great care before delegating control of Active Directory objects, especially the Sites container.

![](img/763d5ae436311371600c0952a3da9094_403_0.png)

![](img/763d5ae436311371600c0952a3da9094_403_1.png)

### TIPS

### Should I delegate control of the Sites container to a group?

Who you delegate control to depends a lot on the organizational structure of your company. Generally, one or two people should be in control of the Sites container rather than a group of people. Because configuration of the sites and site links is crucial for Active Directory communication and replication, you should be careful who is delegated control of the container, and those who do have control should be properly trained.

![](img/763d5ae436311371600c0952a3da9094_404_0.png)

![](img/763d5ae436311371600c0952a3da9094_404_1.png)

- In the **Users or Groups** window, you must specify the user or group you want to Delegate control to.
- Click **Add**.
- Select the user or group you want to delegate control to.
- Click **Add**.
- Click **OK**.

## DELEGATING CONTROL OF THE SITES CONTAINER CONTINUED

After you determine who you will delegate control to, you can further refine the actions that person or group can take. The delegation wizard enables you to specify what permissions that person or group has for the Sites container. This feature is useful because you can delegate certain responsibilities to a group or a user and not others. In other words, this feature enables you to delegate control but also maintain your own level of control over the Sites container as needed.

Keep in mind that when you delegate an OU for a container, such as the Sites container, you are not simply turning over control to another administrator or group of administrators. Delegation is a powerful tool that enables you to assign tasks to different individuals. In this manner, you can allow one person to add objects to the Sites container, but not delete them.

![](img/763d5ae436311371600c0952a3da9094_405_0.png)

- The user or group you choose to delegate to now appears in the list.
- Click Next to continue.
- Click the appropriate radio button to set the rights you want to delegate.
- If you choose to delegate control of specific objects, click the appropriate check boxes to choose the objects.
- Click Next to continue.

![](img/763d5ae436311371600c0952a3da9094_406_0.png)

### What permissions should be assigned?

If you want the delegate to be able to perform any action with the Sites container, then the delegate should be given full control permission. With full control, however, the delegate can make any change he or she desires. If you choose to limit the permissions, you should carefully consider what permissions you assign. Remember that these permissions restrict what the delegate can do, so you do not want to be so restrictive that the delegation has no purpose, yet you do want to be restrictive enough to protect any actions you do not want the delegate to perform.

### Do I have to use delegation?

No. Delegation is provided in Windows 2000 as a tool you can use to reduce administrative overhead. With the often overwhelming amount of work administrators must perform on a daily basis, delegation enables you to assign tasks to other individuals.

![](img/763d5ae436311371600c0952a3da9094_406_1.png)

![](img/763d5ae436311371600c0952a3da9094_406_2.png)

- Use this window to assign the permissions you want to delegate.
- Click the appropriate check boxes for the permissions you want to show.
- Click the appropriate check boxes for the permissions you want to assign for the delegate.
- Click Next to continue.
- A summary window appears.
- Review your settings and click Finish.

![](img/763d5ae436311371600c0952a3da9094_406_3.png)
