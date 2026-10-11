$ net getlocalsid <DOMAINNAME>

on the Samba PDC as root.

Under Samba-2.x the domain SID can be obtained by executing:

$ smbpasswd -S <DOMAINNAME>

The old sambaAccount schema may still be used by specifying the ldap sam.compat passdb backend. However, the sambaAccount and associated attributes have been moved to the historical section of the schema file and must be uncommoned before use if needed. The Samba-2.2 object class declaration for a **sambaAccount** has not changed in the Samba-3 **samba.schema** file.

Other new object classes and their uses include:

+   - **sambaDomain** — domain information used to allocate RIDs for users and groups as necessary. The attributes are added in the “ldap suffix” directory entry automatically if an ldap UID/GID range has been set and the “ldap sam” passdb backend has been selected.
+   
+   - **sambaGroupMapping** — an object representing the relationship between a posixGroup and a Windows group/SID. These entries are stored in the “ldap group suffix” and managed by the “net groupmap” command.
+   
+   - **sambaUNIXIdPool** — created in the “ldap idmap suffix” entry automatically and contains the next available “idmap UID” and “idmap GID”.
+   
+   - **sambaIdmapEntry** — object storing a mapping between a SID and a UNIX UID/GID. These objects are created by the idmap_ldap module as needed.

# ## 34.4.4.2  New Suffix for Searching

The following new **smb.conf** parameters have been added to aid in directing certain LDAP queries when **passdb backend = ldap:sam://...** has been specified.

+   - **ldap suffix** — used to search for user and computer accounts.
+   
+   - **ldap user suffix** — used to store accounts.
+   
+   - **ldap machine suffix** — used to store machine trust accounts.
+   
+   - **ldap group suffix** — location of posixGroup/sambaGroupMapping entries.
+   
+   - **ldap idmap suffix** — location of samaldIdmapEntry objects.

If an *ldap suffix* is defined, it will be appended to all of the remaining subsuffix parameters. In this case, the order of the suffix listings in *smb.conf* is important. Always place the *ldap suffix* first in the list.