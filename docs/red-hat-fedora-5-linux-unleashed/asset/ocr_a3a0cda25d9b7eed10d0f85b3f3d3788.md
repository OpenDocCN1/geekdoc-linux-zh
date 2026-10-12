If you install Samba using your Fedora DVD, you can find a large amount of documentation in the directory tree starting at /usr/share/doc/samba*/doc/ in several formats, including PDF, HTML, and text, among others. Altogether, almost 3MB of documentation is included with the source code.

After Samba is installed, you can either create the file /etc/smb.conf or use the smb.conf file supplied with Samba, which is located by default under the /etc/samba directory with Fedora. Nearly a dozen sample configuration files can be found under the /usr/share/doc/samba*/examples directory.

![](bbox=[0.15, 0.29, 0.87, 0.38])

# ### Manually Configuring Samba with /etc/samba/smb.conf

The /etc/samba/smb.conf file is broken into sections. Each section is a description of the resource shared (share) and should be titled appropriately. The three special sections are

+   - [global]—Establishes the global configuration settings (defined in detail in the smb.conf man page and Samba documentation, found under the /usr/share/doc/samba*/docs directory)

+   - [homes]—Shares users' home directories and specifies directory paths and permissions

+   - [printers]—Handles printing by defining shared printers and printer access

Each section in your /etc/samba/smb.conf configuration file should be named for the resource being shared. For example, if the resource /usr/local/programs is being shared, you could call the section [programs]. When Windows sees the share, it is called by whatever you name the section ([programs] in this example). The easiest and fastest way to set up this share is with the following example from smb.conf:

```
```
[programs]
path = /usr/local/programs
writeable = true
```
```

This bit shares the /usr/local/programs directory with any valid user who asks for it and makes that directory writable. It is the most basic share because it sets no limits on the directory.

Here are some parameters you can set in the sections:

+   - Requiring a user to enter a password before accessing a shared directory

+   - Limiting the hosts allowed to access the shared directory