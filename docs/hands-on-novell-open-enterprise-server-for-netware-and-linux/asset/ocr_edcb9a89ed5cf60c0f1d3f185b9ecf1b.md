With the **Create [C] right** to a directory, users can create new files and subdirectories in that directory. Having only the Create right to a directory enables users to copy files into the directory as long as no other file in the directory has the same name, and having the Create right to a shared directory allows users to copy or create new files in the directory and create subdirectories. Having the Create right to an existing file might seem redundant, but it means that users can salvage the file if it's deleted.

In addition to erasing files, the **Erase [E] right** to a directory allows users to remove the entire directory and its subdirectories. Notice the difference between the Write and Modify rights: The **Write [W] right** grants the privilege of changing or adding data to an existing file, but the **Modify [M] right** allows users to change only a file’s name or attributes, not its contents.

As its name implies, the **Access Control [A] right** allows users to grant access rights to other users to control which users have access to a certain directory or file. However, allowing users to grant rights to other users can make it difficult for a network administrator to keep track of file system security, so the Access Control right shouldn't normally be given to other users.

Having the **Supervisor [S] right** is different from having all rights because it can't be changed or blocked at a lower-level directory or file, and it can be assigned only by another user who has the Supervisor right to the directory. Having the Access Control right doesn't allow users to assign the Supervisor right to themselves or to another user. The Supervisor right is often granted to workgroup managers so that they can control some section of the file system's directory structure. For example, if Kari Means is the workgroup manager for the Engineering Department, she could be granted the Supervisor right to the CORP:\Engineer directory structure.

![](bbox=[0.08, 0.43, 0.92, 0.52])

To help you better understand which access rights are necessary for carrying out functions in the network file system, Table 6-2 lists typical operations users need to perform on files and directories and the access rights required for those operations.

# Table 6-2 Rights required for common functions

| Task | Rights Required |
|---|---|
| Read a file | Read |
| View a directory listing | File Scan |
| Change the contents of data in a file | Write |
| Write to a closed file using a text editor that creates a backup file | Write, Create, Erase, Modify (not always required) |
| Run a program file | Read |
| Create and write to a new file | Create |
| Copy a file from a directory | Read, File Scan |
| Copy a file into a directory | Create |
| Copy multiple files to a directory with existing files | Create, File Scan |
| Create a subdirectory | Create |
| Delete a file | Erase |
| Salvage deleted files | Read and File Scan on the file; Create in the directory or on file name |
| Change attributes | Modify |
| Rename a file or subdirectory | Modify |
| Change the Inherited Rights Filter | Access Control |
| Make or change a trustee assignment | Access Control |