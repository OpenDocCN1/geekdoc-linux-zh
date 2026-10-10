To share files with Samba, you must create file share definitions. These can be as simple as a share name in square brackets in the **smb.conf** file:

```
```
[sample]
```
```

This line creates a share called SAMPLE. If no other lines are present until the end of the file or the next share definition, the share is read-only and provides access to the **/tmp** directory. To make the share useful, chances are you'll want to change at least some of these defaults:

```
```
[sample]
  comment = Sample Samba Share
  path = /home/samba/sample
  read only = No
```
```

This example sets three parameters. The **comment** line sets a comment string that's associated with the share and that appears in many clients' network browsers. It doesn't directly affect the share's functionality, but providing a descriptive comment can help users find the shares they need. The **path** parameter tells Samba what directory to share. The default value is **/tmp**, but that's not usually very useful. A synonym for this parameter is **directory**. Finally, setting **read only** = **No** tells Samba that users may write to the share. The **writable**, **writable**, and **write** ok parameters are antonyms for **read only**; that is, **writable** = **Yes** is equivalent to **read only** = **No**. An important caveat about Samba's write permissions is that they still work within the constraints of Linux file permissions, as described in Chapter 2. Every user who accesses a Samba server does so as an ordinary user. If that user can't write to a directory or file, Samba won't permit the user to do so (at least, not without using more advanced parameters). Thus, you must ensure that **permissions** are set appropriately within file shares if you want your users to be able to write to them. In fact, **permissions** must be set to enable users to **read** files in shares that they should be able to read, as well. In most cases, **0644** (-rw-r--r--) permissions do nicely for files in read-only shares, but managing permissions in read/write shares can be complex.

An important special Samba share is the **[homes]** share. Unlike most shares, this one doesn't point to a single directory; it points to the user's home directory, as defined in **/etc/passwd**. If you want users to be able to store their personal files on a Samba server, a **[homes]** share can be just the thing you need. Most **smb.conf** sample files include a working **[homes]** share, so you might not need to do anything to add one. In operation, this share appears as the user's username\mdash for instance, the user **john** sees a share called **JOHN**.

![](bbox=[0.18, 0.78, 0.26, 0.88])

> > Samba is a very complex and powerful server, and this description barely presents the most basic Samba information. If you need to do more with Samba, you should consult its copious documentation or a book on the subject, such as my *Linux Samba Server Administration* (Sybex, 2001).