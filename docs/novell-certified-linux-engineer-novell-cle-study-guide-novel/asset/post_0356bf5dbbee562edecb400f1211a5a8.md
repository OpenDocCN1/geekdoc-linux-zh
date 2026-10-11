
That’s it! You now have a fully functioning NNLS system and you know how to use Red Carpet to download and apply updates to your system. You’ll spend the rest of this chapter learning how to administer the eDirectory service that was installed on your system.

## Managing eDirectory

**Test Objectives Covered:**

- 3. Describe the purpose of eDirectory.
- 4. Describe how eDirectory works.
- 5. Perform eDirectory administration tasks.
- 6. Manage User objects with iManager.

Up to this point, we’ve briefly brushed up against the topic of eDirectory several times. Each time I’ve said, “Don’t worry, we’ll discuss this in detail later.” Fortunately, later is finally here. It’s time to talk eDirectory.

It is absolutely critical that you master the concepts and skills presented in this part of this chapter. As we will discuss in a minute, eDirectory is the backbone of NNLS. If you don’t understand eDirectory, you won’t be able to manage an NNLS system effectively.

Even if you are already familiar with eDirectory, I would strongly suggest that you read this content anyway. Chances are you learned eDirectory (or its predecessor Novell Directory Services) on the NetWare platform. Most of the concepts are the same with eDirectory on Linux. There are, however, some key differences that can trip you up if you’re not aware of them.

Without any more delay, let’s dig into the world of eDirectory.

## What Is a Directory Anyway?

If you’re new to eDirectory, you may be asking, “What’s this directory thing all about, anyway?” If you learned to manage user accounts using Windows NT domains or Linux passwd files, you’ll be surprised at what you can do with directory services.

Essentially, a directory service is a hierarchical database that is used to store information about network resources.

> **NOTE** The directory services we are discussing here are those that are based on the X.500 directory service standard. You may hear these types of directories referred to as *full-service directories*. Many software vendors over the years have tried to pass off their flat-file user databases as "directories."

The first time I heard the term *directory*, back in the mid-1990s, the image of a phone book came to my mind. That analogy isn't far off. A full-service directory, however, can store more than just user information.

Let's take a few steps back into history. Recall that in an earlier chapter I related a story about my first networking job where I was responsible for an organization's NetWare 3 network.

NetWare 3 (and earlier versions of NetWare as well) used a flat-file database called the *bindery* to store user accounts and groups. Each server in my network had its own bindery. My organization had about 1200 users, each with his or her own account. Each needed access to resources hosted by each of the NetWare servers I was responsible for.

That required me to keep the user accounts and passwords synchronized on all servers in the organization. Needless to say, for the first couple of months on the job, that's about all I did. My users simply expected to have a single password to access all network resources.

If they changed their password in one bindery user account, they expected that password to work when accessing other servers in the network. Eventually, that would be so, but only after I fielded their complaint and manually changed the account information on the other servers.

After a couple of months, I became very annoyed with the situation and wrote some nifty little programs that could be used to synchronize accounts between servers; but it was still a manual process. If I forgot to run them, the accounts would quickly go out of sync and the help desk calls would start rolling in.

This situation also presented a problem when a new individual would join or leave the organization. I had to either create multiple accounts or delete multiple accounts on all the servers.

In addition, each version of the user's account had different trustee assignments and login scripts. Talk about job security.

If you've ever managed a Linux network that employed multiple servers, you've faced a similar issue. Remember that Linux users and groups are local to the server. To get around this, many Linux administrators employ the NIS+ service, which synchronizes user accounts among Linux servers. eDirectory changes all that. With this service, all the servers on your network are installed into the eDirectory tree. User accounts are also created in the tree. Users have one single account that gives them access to network resources.

Instead of logging in to a specific server, users authenticate to the eDirectory tree. From there, they can access any network data or resource they have been granted access to, regardless of what server is hosting the resource.

In addition, applications can be easily written that access directory information. As you will see later in this book, all NNLS components do just that. They use eDirectory information to control access, display information, and provide services.

eDirectory fills the following primary roles:

- Storing network data in a central repository
- Organizing network data into a logical structure
- Providing standardized methods for accessing network data
- Controlling access to network data
- Securing network data

Let’s now discuss how eDirectory works.

## How eDirectory Works

When discussing how eDirectory works, we’re going to stay at the conceptual level. Recently, I had the opportunity to spend time with the software developers at Novell who actually wrote the eDirectory code, learning about the inner workings of the product. My head was swimming after only a few minutes (and I had considered myself an eDirectory veteran!). We will discuss the following topics:

- The structure of the eDirectory tree
- How eDirectory naming conventions work
- How eDirectory rights work
- How eDirectory embraces the Lightweight Directory Access Protocol (LDAP) standard

## The Structure of the eDirectory Tree

Recall that I mentioned earlier that eDirectory is a hierarchical database. Before discussing what this is, let’s talk about what it is not.

Windows NT domains, the Linux passwd file, and NetWare binderies are all considered flat-file databases (that is, nonhierarchical). This is because entries in these databases can’t contain other database entries.

Many new to directory services contend that this isn’t entirely true because, they argue, groups in these databases are composed of user accounts. This isn’t correct. A group in one of these databases has users who are *members* of the group. The actual user account itself resides outside the group; user accounts aren’t actually contained *within* the group.

The hierarchical eDirectory database, on the other hand, handles things in a very different manner. You must first understand that entries in the eDirectory database are called *objects*. There are two general categories of objects within the database:

- **Container objects**—Container objects can contain other database objects. To draw a simple comparison, container objects are similar to directories within a file system. File system directories can contain files or other directories.
  - Likewise, an eDirectory container object can contain other container objects, or *leaf objects*. Container objects are used to organize directory data. Container objects can be used to organize data by geographical location, business unit, or organizational function.
- **Leaf objects**—Leaf objects represent network resources in the eDirectory database. These can be physical resources, such as users, printers, and servers. Or, they can be logical network resources such as groups, profiles, and templates.
  - Carrying on the analogy started earlier, leaf objects are similar to files within the file system. In the file system, files contain real data. Files can’t contain directories or other files.
  - Likewise, leaf objects in the eDirectory database can’t contain any other objects.

All eDirectory objects, both container and leaf, are contained within the eDirectory tree. Each eDirectory tree has a set of rules that defines the types of objects that can exist in the tree and where they can reside. This set of rules is called the *schema*. A very simple eDirectory tree is shown in Figure 5.28.
