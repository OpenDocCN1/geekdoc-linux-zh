
## CHAPTER SUMMARY

- Just as a building needs to be secured by using locks and keys, the NetWare file system must be secured by using trustee assignments to grant rights that allow users to access the storage areas they need. NetWare has eight access rights: Read, File Scan, Write, Create, Erase, Modify, Access Control, and Supervisor.

- The Access Control right allows users to assign other rights, except Supervisor, to other users. The Supervisor right can be assigned only by a Supervisor-equivalent user and gives users all rights to a directory and its subdirectories, including the right to assign the Supervisor right to other users. In addition, because the Supervisor right can’t be revoked or blocked at lower levels, assigning the Supervisor right is a good way to make a user act as a supervisor of a portion of the directory structure.

- Trustee assignments are used to grant rights to users or groups for a directory. Effective rights for a user are a combination of the user object’s rights and the rights given to any groups of which the user is a member. A user or group’s trustee assignments for a directory are then inherited by all the subdirectories and files in the directory where the trustee assignment was made. A user’s effective rights often include inherited rights from a trustee assignment made to a group or user in a higher-level directory.

- Each directory and file has an Inherited Rights Filter (IRF) to control which rights it inherits from higher-level directories. When a file or directory is first created, the IRF allows all rights to flow down to that directory or file. You can use an IRF to block the directory or file from inheriting those rights.

- You can use ConsoleOne, Remote Manager, Windows Explorer, or the RIGHTS command to set and view trustee assignments.

- Attributes play a vital role in file system security because they enable you to protect files and directories from certain operations, such as deleting, renaming, and copying.

- You can use Remote Manager, ConsoleOne, and the FLAG command to set attributes on files and directories.

## KEY TERMS

**Access Control [A] right** — An access right that allows a user to grant access rights for a directory to other users.

**access right** — A file system permission that can be granted to users, groups, or containers. Access rights include Supervisor, Read, Write, Create, Erase, Modify, File Scan, and Access Control.

**Archive Needed (A)** — A file attribute that indicates the file has been changed since it was last backed up.

**attribute** — A flag or code associated with files and directories to control what type of processing can be performed on them.

**Copy Inhibit (Ci)** — A file attribute that prevents Macintosh computers from copying the file.

**Create [C] right** — An access right that allows users to create files and subdirectories.

**Delete Inhibit (Di)** — An attribute that protects a file or directory from being deleted.

**directory entry table (DET)** — An area of the hard drive containing information about files and directories, including name, location, and trustee assignments.

**directory trustee** — A user, group, or container object that has been granted access rights to a directory.

**Don’t Compress (Dc)** — A file attribute that tells the operating system not to compress the file. When applied to a directory, none of the files in the directory will be compressed.

**Don’t Migrate (Dm)** — A file or directory attribute that prevents files or directories from being migrated to a high-capacity storage device.

**Don’t Suballocate (Ds)** — A file attribute that tells the operating system not to use block suballocation on the file.

**effective rights** — A subset of access rights that controls which functions a user can perform in a directory or file.

**Erase [E] right** — An access right that allows the user to delete files and remove subdirectories.

**Execute Only (X)** — A file attribute that can be applied to .com and .exe files to prevent them from being copied. Once applied, the Execute Only attribute can't be removed.

**File Scan [F] right** — An access right that allows the user to view a directory of file and subdirectory names.

**File trustee** — A user, group, or container object that has been granted access rights to a file.

**Hidden (H)** — A file or directory attribute that prevents standard DOS and Windows applications from seeing the associated file or directory.

**Immediate Compress (Ic)** — A file or directory attribute that tells the system to compress a large file immediately after it has been used.

**Inherited Rights Filter (IRF)** — A method of reducing inherited rights in a subdirectory or file by allowing only the access rights specified in the filter to be inherited.

**Migrated (M)** — A file attribute set by the system indicating that a file has been moved to an archive data medium.

**Modify [M] right** — An access right that allows the user to change file and directory names—without changing the file contents—and use the FLAG command to change attribute settings on files or subdirectories.

**Normal (N)** — A directory attribute that removes all other directory attributes.

**Purge (P)** — A file or directory attribute that prevents files in a directory from being salvaged after deletion.

**Read [R] right** — An access right that allows the user to read files or run programs in a directory.

**Read Only (Ro)** — A file attribute that prevents the contents of a file from being modified.

**Read Write (Rw)** — A default file attribute that allows the contents of a file to be changed.

**Rename Inhibit (Ri)** — A file or directory attribute that prevents the name of a file or directory from being changed.

**Sharable (Sh)** — A file attribute that allows multiple users to use a file at the same time.

**Supervisor [S] right** — An access right that grants all rights to a directory and its subdirectories; this right cannot be blocked or reassigned at a lower subdirectory or file level.

**System (Sy)** — A file or directory attribute that flags a file or directory for operating system use.

**Transaction Tracking System (TTS)** — A system that protects the Transactional attribute, ensuring that all transactions are completed or left in the original state.

**Transactional (T)** — A file attribute used on database files to enable the system to restore the file to its previous state if a transaction is not completed.

**trustee assignment** — An entry in the ACL for a file or directory that makes the user a trustee of a directory or file.

**Write [W] right** — An access right that allows the user to change or add data to files in a directory.

## REVIEW QUESTIONS

1. Which of the following defines file system functions that users can perform in the NetWare file system?
   - a. attributes
   - b. access rights
   - c. eDirectory
   - d. NSS

2. Which of the following rights allows a user to change data in an existing file?
   - a. Modify
   - b. Write
   - c. Create
   - d. Access Control

3. Which of the following rights allows a user to assign rights to other users?
   - a. Modify
   - b. Write
   - c. Create
   - d. Access Control

4. Which of the following rights can't be revoked or blocked in the directory structure it defines?
   - a. Modify
   - b. Supervisor
   - c. Create
   - d. Access Control

5. Which of the following are flags that control directory and file characteristics?
   - a. attributes
   - b. properties
   - c. rights
   - d. permissions

6. You are a member of the Admin group that has been granted [R W F] rights to the Business directory, and you have a trustee assignment of [R C F] to that directory. What are your effective rights in the Business directory?

7. You have been given a trustee assignment of [R C F] to the Business directory and a trustee assignment of [W E] to the Business\Sdata\Budgets subdirectory. What are your effective rights in the Business\Sdata subdirectory?

For Questions 8 through 11, use the following file system information:
You have a trustee assignment of [W E C] to the Business directory and a trustee assignment of [W E] to the Business\Sdata\Budgets subdirectory. In addition, you belong to a group that was granted [R F] rights to the Business directory.

8. What are your effective rights in the Business\Sdata\Budgets subdirectory?

9. Assume that all rights except [R] and [F] are removed from the [R F] of the Business\Sdata subdirectory. What are your rights in the Business\Sdata subdirectory?

10. What are your rights in the Business\Sdata\Budgets subdirectory?

11. Write the command to list all trustee assignments in the Business directory structure.

12. The user Joeman was given a trustee assignment of [R W E C M F] to the Business\Sdata directory and a trustee assignment of [R W F] to the Business\Sdata\Budgets subdirectory. What are Joeman's effective rights in the Business\Sdata\Budgets subdirectory after deleting his trustee assignment to the Budgets directory?

13. Did Joeman gain or lose rights in the Budgets directory? Why?

14. If you're using Windows, which of the following utilities could you use to make the user Billsim a trustee of the Business\AR directory? (Choose all that apply.)
    - a. Windows Explorer
    - b. iManager
    - c. ConsoleOne
    - d. Remote Manager
