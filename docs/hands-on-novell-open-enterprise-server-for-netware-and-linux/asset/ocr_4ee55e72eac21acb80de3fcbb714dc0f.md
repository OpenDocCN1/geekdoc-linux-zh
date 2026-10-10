# **Directory Design Form**

Designed by: **Eric Kenton**  Date: ________  
Volume name: **CORP** Directory Name: **Engineer** Estimated Size: **18 GB**

![](bbox=[0.08, 0.14, 0.73, 0.36])

# **Figure 3-26 A sample Directory Design Form for the Engineering Department**

The directory structure Eric used is referred to as a **departmental structure** because the user home directories, shared directories, and applications are located within the departments that control them. Directories containing files available to all users, such as Forms and Inventory, are located at the root of the volume. Shared directories are located within each department’s directory to provide separate shared file access for all users in the department. The Shared directory off the root of the CORP volume is available so that users in all departments can exchange files or work on common projects. For example, the Engineering Department can use the CORP:Shared directory to save files the Desktop Publishing and Sales employees need to prepare documentation and presentations.

Another way to organize directories on a volume is by application rather than by department. Figure 3-27 shows an example of how the directories of a universal AeroSpace might be organized in an application-oriented structure.

Notice that in an **application-oriented structure**, all user home directories are placed under a common directory called Users. Shared directories can then be grouped according to their use, and applications can be placed in separate directories under the root of the volume. The advantage of an application-oriented structure is that it’s fairly shallow, making it easier to locate files without going through several layers of directories. In larger directory structures, however, this shallow nature can actually be a disadvantage, making it difficult to know which departments use which directories. When using an application-oriented structure, a network administrator needs to make more trustee assignments because a user’s rights don’t flow automatically into other directories. In Chapter 6, you learn how to make trustee assignments that grant users rights to the directory structure.

The organization method you select for a directory structure depends on personal preference, the organization’s size, and the way users access data. Generally, smaller network file systems are easier to organize by using an application-oriented structure because it keeps the design simple and easy to use. With larger file systems that encompass several departments and many data directories, often a departmental structure makes it easier to maintain security and locate data. In some cases, you might find that a combination of both structures works the best. No matter what design method you use, a good rule of thumb is not to exceed three subdirectory layers, with no more than 20 subdirectories in any one directory (which makes it easier to view all directories onscreen at the same time).