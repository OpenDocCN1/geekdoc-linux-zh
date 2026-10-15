
be included. A need might also arise for performance-related tasks, such as adjusting WLM policies.

For most z/OS sites, these tasks are performed by different lines or departments within the organization.

## 6.2.2 Defining users in z/VM

This section discusses how users are defined to z/VM. For more details about how to do this, see Chapter 4, "Installing z/VM and creating Linux or z/OS guests" on page 121.

### USER DIRECT file

The z/VM users all have to be defined and maintained in the file USER DIRECT (provided DIRMAINT and RACF are not installed). This file exists in two forms: in one or more source forms on one or more CMS files; and in a compiled object form on a CP-formatted disk. Only one USER DIRECT can be active at any given instant, but multiple can be accessed. The USER DIRECT is read at IPL time in a predefined search order. First, the system residence volume is searched for a valid object entry. If no such entry exists, all CP-owned volumes are searched, in the order in which they appear (in the CP-owned list). If CP cannot find a valid object, z/VM constructs a default user ID of OPERATOR. By logging on to this user, you can then establish valid USER DIRECT object.

### Source formats of USER DIRECT

The source version of USER DIRECT can exist in two formats: monolithic, in which all statements are contained in one physical file; cluster form, which includes an index file that can point to one or several files containing the necessary statements to build an object USER DIRECT file.

> Note: All references to USER DIRECT in this book is for the monolithic source format. For further details on the cluster format, refer z/VM: CP Planning and Administration, SC24-6083.

### Defining minidisks

User data in z/VM is divided into the minidisk entity. This implies dividing your disk volumes into physical extents with a starting cylinder address and counting the number of cylinders from that.

## 6.2.5 DISKMAP command

This command is used to map the disk extents of the z/VM disks. In this section, we pay attention to the disk containing user minidisks, because we are going to define a new CMS user.

> Important: Use of the DISKMAP command is optional, but it is highly recommended.

DISKMAP reports any gaps or overlaps on these disks. Gaps imply that you are not using the disk fully, whereas overlaps means that users are using the same extent of the disk. The latter implies a potential risk of overwriting data, thus corrupting the disks, and should therefore be avoided.

The command is invoked by issuing:

```
DISKMAP fn ft (DOENDS
```

The fn is the file name of the USER DIRECT source you want to examine, and ft is its file type. The ending text, DOENDS, causes MDISK statements, which had "END" specified for the ending cylinder/block in the directory being mapped, to be included in the DISKMAP output file.

Output from DISKMAP is stored in file DISKMAP (fn is the filename of the mapped file) on the A drive of the user running it.

To run the command diskmap user, users must have at least privilege class B.

Figure 6-1 on page 297 shows the output of file USER DISKMAP A (the output is lengthy so lines have been removed from the figure). Notice the GAP on line 00329 starting at cylinder 1886 for 114 cylinders and ending at 1999.

Based on the output from DISKMAP, minidisks for the user to be defined would have to start in CYLINDER 2380 so that no overlaps result (see line 00337 for LYDIA 191 ending in cylinder 2379).

It is a good idea to perform a syntax check of the contents of the source file (and run the DISKMAP command to check for possible disk overlaps; see 6.2.5, "DISKMAP command" on page 296).

The syntax for the DIRECTXA command is explained in Figure 6-2.

![](img/b0a4b9056f819dccd4781a5105c92d45_313_0.png)

Figure 6-2 Syntax for DIRECTXA command

Note that filename (fn) and file type (ft) have default values of USER and DIRECT, respectively. Therefore, the following commands work the same, if you prefer a different name for the source version of the file (provided files MYDIR DOCUMENT and MYDIR DIRECT exist):

```
DIRECTXA MYDIR DOCUMENT
```

```
DIRECTXA MYDIR
```

To check the syntax of the edited source file, issue the command:

```
DIRECTXA fn ft * (EDIT
```

This is a useful function, especially for personnel with limited experience in maintaining this type of file.

As an example, the source file (MYDIR DOCUMENT) contains the statement shown in Figure 6-3 on page 299. Instead of LINK, the administrator entered LUNCH.
