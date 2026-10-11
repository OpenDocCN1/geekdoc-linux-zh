# 15.3 Share Definition Access Controls

The following parameters in the **smb.conf** file sections define a share control or affect access controls. Before using any of the following options, please refer to the man page for **smb.conf**.

# 15.3.1 User- and Group-Based Controls

User- and group-based controls can prove quite useful. In some situations it is distinctly desirable to force all file system operations as if a single user were doing so. The use of the *force user* and *force group* behavior will achieve this. In other situations it may be necessary to use a paranoiac level of control to ensure that only particular authorized persons will be able to access a share or its contents. Here the use of the *valid users* and the *invalid users* parameter may be useful.

As always, it is highly advisable to use the easiest to maintain and the least ambiguous method for controlling access. Remember, when you leave the scene, someone else will need to provide assistance, and if he or she finds too great a mess or does not understand what you have done, there is risk of Samba being removed and an alternative solution being adopted.

Table 15.2 enumerates these controls.

# 15.3.2 File and Directory Permissions-Based Controls

Directory permission-based controls, if misused, can result in considerable difficulty in diagnosing the causes of misconfiguration. Use them sparingly and carefully. By gradually introducing each, one at a time, undesirable side effects may be detected. In the event of a problem, always comment all of them out and then gradually reintroduce them in the controlled way.

Refer to Table 15.3 for information regarding the parameters that may be used to set file and directory permission-based access controls.

# 15.3.3 Miscellaneous Controls

The parameter documented in Table 15.4 are often used by administrators in ways that create inadvertent barriers to file access. Such are the consequences of not understanding the full implications of **smb.conf** file settings.

# 15.4 Access Controls on Shares

This section deals with how to configure Samba per-share access control restrictions. By default, Samba sets no restrictions on the share itself. Restrictions on the share itself can be set on MS Windows NT4/2000/XP shares. This can be an effective way to limit who