
- 2. Insert new files into the RCS system. Using the ci command, check files into your RCS directory.
- 3. Be sure to “check out” a file before editing it. Use the co command before you begin to edit the file.
- 4. Use “check in” after changes are complete. Once you have completed your modifications, be sure to check in your changes, or they will be lost the next time someone edits the file.
- 5. When needed, enable previous versions of the modified file. You have the option of choosing any previous version to retrieve, using the -r option to co.

Once you’ve downloaded and installed GNU RCS, developing the human processes for using RCS is much more difficult than using the software itself. To begin using RCS in a directory, say /etc/, you’ll need to create the subdirectory /etc/RCS. This subdirectory will store all the changes you check in to specified files. To activate RCS, you must initially check in each file you wish to track. For example, to begin tracking changes to your /etc/hosts file, in the /etc/ directory, type:

```
# ci hosts
```

This will create revision 1.0 of /etc/hosts in the /etc/RCS directory. However, don’t edit any files in the RCS directory! To begin editing a file, you should check it out and lock the file. The process of locking a file gives ownership to the user with the lock, and prevents other users from overwriting any changes. For system files, or when multiple users will interact with a file, locking is essential. Failure to lock a file can cause multiple users to overwrite each other’s changes if they are working on that file at the same time.

To check out a file, type:

```
# co -l hosts
```

The -l option locks the file and gives ownership to the user checking it out. The file you should now edit is /etc/hosts. Anyone else editing the /etc/hosts file without using RCS will have their changes lost once you check in /etc/hosts using:

```
# ci -u hosts
```

The -u option unlocks the file so that others can now edit the file. Failure to use the -u option will keep /etc/hosts locked and only editable by the user who checked it out.

In time, you’ll want to bring back earlier versions of a file to correct some problems, or retrieve some information that was previously deleted. To check out the most recent version, type:

```
# co -r hosts
```

and this will recover to the last /etc/hosts version that was checked in. To recover to previous versions, you can give a version number such as:

```
#co -r1.12 hosts
```

This will restore version 1.12 of /etc/hosts for editing. If you choose to keep version 1.12 as your current version, just check it in again, and it will become your current version.

RCS, like other version control software, is very powerful and offers more options and tools than can be discussed here. However, the most important point you should take from this section is that you have to buy into using version control 100% of the time, or it becomes ineffective. The most common problem is the failure to check out a file in the first place, where an administrator edits a file as root, saves it, and then someone else, or the same administrator, then uses RCS to manage the file. All the changes that were input during the non-RCS sessions will be lost, with no hope of recovery. Once you’ve lost an hour’s worth of changes the first time, you’ll better understand the rigor needed to use RCS. However, good practices started early can save you hours of replicating work later.

> ci, co-Check in and check out, respectively. These are part of the suite of commands that make up the RCS version control system.

## Distributing Files and Applications

Moving files from one place to another can be a tedious task. Before the introduction of the Internet and local networks, moving files from one system to another required copying data to a transportable device such as a tape or floppy disk. This method was quite effective for small amounts of data, but not very useful for large amounts of data, or in situations where you needed information transferred quickly. In this section, you will be presented with some tools and processes that take advantage of system utilities, as well as the network, to keep your files moving freely and make your users more productive.

## UNIX FILE MANAGEMENT TOOLS

Managing UNIX files can be simple or complex, depending on the functionality you choose to build into your process. In the following sections, you will be presented with a few of the simpler, yet more powerful tools for managing UNIX files. These tools can be broken into two categories: those that work over NFS or on the local system, and those that work with remote systems where NFS file sharing is not an option. For NFS or local systems,
