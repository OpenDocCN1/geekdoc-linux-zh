# FIGURE 11.27
The default  
/etc/security/or 
of_attr file

![](bbox=[0.26, 0.12, 0.95, 0.38])

Profiles stored in the prof_attr file can contain the access granted in the auth_attr file as well as commands that have the attributes for the profile that are contained in the exec_attr file. Entries in the prof_attr database are named profiles, their descriptions, along with their attributes. The five fields in the prof_attr file take the form profname:reserved1:reserved2:description:attribute list. (To continue a line in this file, use the backslash symbol). The case-sensitive profname field is the name of the profile, used to identify it to programs. The terms reserved1 and reserved2 are not currently assigned; they are reserved for future use. The description field is used to provide a description of the profile and the type of user who might use the authorization. The important variable here (as before) is the attribute list, which is a semicolon-delimited list of key value pairs that apply a security level to an object when it is executed.

For example, an entry in the prof_attr file might look like this:

```
Device Management:::Control Access to Removable
Media:auths=solaris.device.*;help=DevMgmt.html
```

When the Device Management profile has been assigned to the sysadmin role in the usr_attr database, you would see the following:

```
root:: :::type=normal,auths=solaris.\*,solaris.grant;profiles=All
advanced:: :::type=role;profiles=Device Management,
Printer Management
```

The profiles are read by the authorizations contained in the auth_attr file, where you will find named authorizations such as solaris.device., solaris.device.allocate, solaris.device.config, solaris.device.grant, and solaris.device.revoke. A typical entry in the auth_attr file would look like the following: