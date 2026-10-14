The format of the homes section is very simple; it starts with the [homes] tag. The next tag you should enter is the comment tag. This is a text comment that can be used to describe the share. So far it should look like this:

```
[homes]
comment = User homes
```

This setting will work fine, but it won't look very good when you browse the machine. When you browse the machine, you will find a share called homes, and if you are a user, you will also find your home directory as a share. For example, a user named John will find two shares, one called homes and another called john. Whereas, a guest user will see only a share called homes. For a user, both shares will point to the same directory—his home directory. If you enter the parameter browseable = no in the homes section, Samba will not show a share called homes. If a user is browsing the machine, he will see a new share that is his home. Guest users will see nothing.

Another decision you need to make is whether you want the users to be able to write to their homes or not. This is accomplished using the read only parameter. Setting this parameter to yes, which is its default, will prevent users from writing in their home directory through Samba. Setting it to no allows them to write to it.

Another useful parameter is case sensitive. Setting this to yes forces Samba to treat file-names as being case-sensitive. This is useful because Windows is not case-sensitive, and if Samba treats the filenames as case-sensitive, conflicts will arise. Setting this parameter to no will prevent such conflicts.

To hide the share homes, allow users to write to their home directories, and ignore case sensitivity, the code section would look like the following:

```
[homes]
comment = User homes
browseable = no
case sensitive = no
read only = no
```

# The printers Section

This section tells Samba about your printers. You can have Samba put your printer on the network to be shared by others.

This section starts with [printers], followed by a comment that describes it. The next parameter, which is the most important one, is printable. This parameter tells Samba that this share is not a disk share but a printer share. Even though section printers is a special section, you still have to enter printable = yes in it.

If you want guests to be able to print from this printer, you should include guest ok = yes in this section. Another parameter of interest is directory. When Samba receives a print