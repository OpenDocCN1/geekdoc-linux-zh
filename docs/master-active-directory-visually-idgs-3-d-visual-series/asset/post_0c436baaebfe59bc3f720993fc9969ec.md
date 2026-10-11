
## What is a Description Bar?

The Description Bar—a small tool bar that appears over the MMC details pane—is an option you can select from the View menu. When you select different items, a description of the item appears in the toolbar. The Description Bar may be a helpful feature to use as you are learning to work with the MMC.

## What are favorites?

Favorites are simply snap-in or child containers you select in the MMC windows and mark as a "favorite." A favorite is normally something you use often and want to access easily from the Favorites menu.

## What can be a favorite?

Any snap-in or child container of a snap-in (as well as the root container) can be a favorite. Basically, you can select anything you see in the console tree and add it to the favorites list.

![](img/763d5ae436311371600c0952a3da9094_280_0.png)

- If you choose **Add To Favorites**, the selected folder or snap-in is added to your favorites list.
- Click **OK** to add it.
- Or, click the **New Folder** button to place your Favorites in a different folder.

![](img/763d5ae436311371600c0952a3da9094_280_1.png)

- Type the name of the new folder.
- Click **OK**.

## ACCESSING THE SEARCH WINDOW

One of the most important components of any directory is finding the information you need. Whether you use a paper directory, such as a phone book, or an electronic directory, such as the Active Directory, success or failure depends on users being able to find the information they need.

The Active Directory stores all information in the global catalog, which contains pointers to the specific objects contained in the directory. You can use the search feature to search the global catalog to find any resource in the Active Directory. Search windows are available within the Administrative tools, but clients access the search function using My Network Places. Because the Active Directory is LDAP (Lightweight Directory Access Protocol) compliant, users can perform keyword searches so they can easily find the kind of information they need. For example, you can search for "printers" in the Active Directory and all available printer objects will be returned.

![](img/763d5ae436311371600c0952a3da9094_281_0.png)

### Tips

**How does Windows search the Active Directory?**
Active Directory searches are performed using the LDAP (Lightweight Directory Access Protocol), a communication protocol used for directory access on TCP/IP networks. LDAP is a more efficient protocol than DAP (Directory Access Protocol) and has been primarily associated with Internet functions. Access to domain controllers and global catalogs is performed using LDAP.

**Can users browse for Active Directory objects?**
Yes. Active Directory users can access My Network Places and browse the domain and OU structure to find resources they need. In small environments, this may work fine, but in Enterprise environments, users should find Active Directory resources using its powerful query capabilities. Users may need to be trained in Active Directory search operations so they can make the most of the Active Directory.

![](img/763d5ae436311371600c0952a3da9094_282_0.png)

- Double-click Directory.

![](img/763d5ae436311371600c0952a3da9094_282_1.png)

- Double-click the domain icon.

### ACCESSING THE SEARCH WINDOW CONTINUED

By accessing the search window, you can then find any object you would like to find within the Active Directory. Because the global catalog uses LDAP, you do not have to know the exact name of an Active Directory object to locate it. LDAP can perform full text searches to help you find certain kinds of objects or close matches to the requests that you need. Because of the structure of the Active Directory and the attributes of Active Directory objects, you can perform a basic search, such as entering a user name or simply searching for "John." In either case, the Active Directory returns all possible matches. You can also perform a text search, which enables you to use a combination of words, such as "company documents and forms," and the Active Directory will use your word search to find possible matches.

![](img/763d5ae436311371600c0952a3da9094_283_0.png)

![](img/763d5ae436311371600c0952a3da9094_283_1.png)

- The Organizational Units (OUs) for the organization appear.
- Select the OU you want to search.
- Choose File→Find.

### Tips

**Do I have to find the OU in which an object is contained to search for it?**

No. This section of the book simply shows you an easy way to access the search window. After you access the search window, you can choose to search for any kind of object within the entire Active Directory as needed. The next section in this chapter shows you how.

**I am in an Enterprise environment. Can I search the entire Enterprise or do I have to search each domain?**

You can search the entire Active Directory for your enterprise. Because the enterprise contains global catalog servers, which hold a “replica” of all Active Directory objects in the entire Active Directory, you can search the entire directory and the global catalog servers will find all objects that meet your search. Of course, in very large environments, narrow your search as much as possible so that you do not have too many match returns.

![](img/763d5ae436311371600c0952a3da9094_284_0.png)

- The search window appears.

![](img/763d5ae436311371600c0952a3da9094_284_1.png)

- To search for the selected category, type a name or description.
- Click **Find Now** to begin the search.

## UNDERSTANDING SEARCH WINDOW BASICS

From the search window, you can specify what Active Directory objects you want to search for and in what location. The In drop-down menu enables you to search for an Active Directory object within a particular container or domain, or you can choose to search the entire directory for the object.

The Find drop-down menu enables you to select the kind of object you want to search for, whether it's a user, folder, OU, printer, or any other Active Directory object. You can also choose to perform a custom search, which allows you to specify what you want to find by using LDAP keywords.

Essentially, the search window allows you to determine what you want to search for and where you want to search for it. You can search for objects at the entire Active Directory level, domain level, or OU level. This feature enables you to have a very broad or very narrow search as desired.

![](img/763d5ae436311371600c0952a3da9094_285_0.png)

- Open the Search window (see the previous task for instruction).
- Click the In drop-down menu to select the location of your search.
    - You can search particular OUs, domains, or the entire directory.
- If the desired location is not available, click Browse to browse for the specific OU or container you want to search.

### TIPS

**Why do I have the option to search within a particular domain or container? Can’t I just search the entire directory?**

Depending on the size of your organization, simply searching the entire directory for the resource you need may be easier. However, in large environments that contain multiple domains and even multiple sites, you can restrict your search to a particular area.

**Why would I perform a search within an OU?**

An OU search is particularly useful if you know that a resource exists in a certain OU, but you do not know the name of the resource. For example, you may know that a certain printer exists in a particular OU, but you do not know the printer’s name. You can use an OU search and simply look for “printers” to find the printer in the OU you want. If you searched the entire directory for the printer, you would have a much lengthier search return list you would have to sort through.

![](img/763d5ae436311371600c0952a3da9094_286_0.png)

- Click the Find drop-down menu to specify the kind of Active Directory object that you want to find.

![](img/763d5ae436311371600c0952a3da9094_286_1.png)

- Optionally, use the Advanced tab to specify search criteria.
