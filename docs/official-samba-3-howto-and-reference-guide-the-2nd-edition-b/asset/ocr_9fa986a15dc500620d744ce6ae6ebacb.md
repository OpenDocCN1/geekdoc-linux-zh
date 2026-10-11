As the examples are developed, every attempt is made to progress the system toward greater capability, just as one might expect would happen in a real business office as that office grows in size and its needs change.

# ### 2.3.1.1 Anonymous Read-Only Document Server

The purpose of this type of server is to make available to any user any documents or files that are placed on the shared resource. The shared resource could be a CD-ROM drive, a CD-ROM image, or a file storage area.

+   - The file system share point will be /export.
+   - All files will be owned by a user called Jack Baumbach. Jack's login name will be jackb. His password will be m0r3p4in — of course, that's just the example we are using; do not use this in a production environment because all readers of this document will know it.

INSTALLATION PROCEDURE: READ-ONLY SERVER

```
**Example 2.3.1 Anonymous Read-Only Server Configuration**
```
# Global parameters
[global]
    workgroup = MIDEARTH
    netbios_name = HOBbit
    security = share

[data]
    comment = Data
    path = /export
    read_only = Yes
    guest_ok = Yes
```
```

+   1. Add user to system (with creation of the user’s home directory):
+      ```
+      root# useradd -c "Jack Baumbach" -m -g users -p m0r3p4in jackb
+      ```
+   2. Create directory, and set permissions and ownership:
+      ```
+      root# mkdir /export
+      root# chmod u+rwX,g+rX,o+rX /export
+      root# chown jackb.users /export
+      ```
+   3. Copy the files that should be shared to the /export directory.
+   4. Install the Samba configuration file (/etc/samba/smb.conf) as shown in Example 2.3.1.
+   5. Test the configuration file by executing the following command: