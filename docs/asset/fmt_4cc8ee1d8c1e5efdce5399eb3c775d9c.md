
Certain privileged programs check the authorizations to determine whether users can execute restricted functionality. For example, the `solaris.jobs.admin` authorization is required for one user to edit another user's crontab file.

All authorizations are stored in the `auth_attr` database. If no name service is used, the database is located in a file named `/etc/security/auth_attr`. Authorizations can be assigned directly to users (or roles), in which case they are entered in the `user_attr` database. Authorizations can also be assigned to profiles, which in turn are assigned to users. They are described in the “Rights Profiles (`prof_attr`) Database” section.

The fields in the `auth_attr` database are separated by colons, as shown here:

```
authname:res1:res2:short_desc:long_desc:attr
```

Each field is described in Table 20.4.

## 表 20.4

### AUTH_ATTR 字段

| Field Name | Description |
|------------|-------------|
| `authname` | A unique character string used to identify the authorization in the format *prefix*.[*suffix*]. Authorizations for the Solaris operating environment use `solaris` as a prefix. All other authorizations should use a prefix that begins with the reverse-order Internet domain name of the organization that creates the authorization (for example, `com.xyzcompany`). The suffix indicates what is being authorized, typically the functional area and operation. When no suffix exists (that is, the `authname` consists of a prefix and functional area and ends with a period), the `authname` serves as a heading for use by applications in their GUIs rather than as an authorization. The `authname` `solaris.printmgr.` is an example of a heading. When `authname` ends with the word *grant*, the `authname` serves as a grant authorization, and allows the user to delegate related authorizations (that is, authorizations with the same prefix and functional area) to other users. The `authname` `solaris.printmgr.grant` is an example of a grant authorization; it gives the user the right to delegate such authorizations as `solaris.printmgr.admin` and `solaris.printmgr.nobanner` to other users. |
| `res1` | Reserved for future use. |
| `res2` | Reserved for future use. |
| `short_desc` | A shortened name for the authorization suitable for displaying in user interfaces, such as in a scrolling list in a GUI. |
| `long_desc` | A long description. This field identifies the purpose of the authorization, the applications in which it is used, and the type of user interested in using it. The long description can be displayed in the help text of an application. |
| `attr` | An optional list of semicolon-separated (`;`) key-value pairs that describes the attributes of an authorization. Zero or more keys can be specified. The keyword `help` identifies a help file in HTML. Help files can be accessed from the `index.html` file in the `/usr/lib/help/auths/locale/C` directory. |

The following are some typical values found in the default `auth_attr` database:

```
solaris.admin.usermgr.pswd:::Change User Passwords::help=UserMgrPswd.html
solaris.system.shutdown:::Shutdown the System::help=SysShutdown.html
solaris.admin.fsmgr.write:::Mount/Share File Systems::help=FsMgrWrite.html
```

Look at the relationship between the `auth_attr` and the `user_attr` databases for the `adminusr` role we added earlier:

```
adminusr::::type=role;auths=solaris.admin.usermgr.pswd, \
solaris.system.shutdown, solaris.admin.fsmgr.write;profiles=All
```

Notice the authorization entries that are bold. These authorization entries came out of the `auth_attr` database, which are shown above. The `solaris.system.shutdown` authorization, which is defined in the `auth_attr` database, gives the role the right to shut down the system.

## 权利配置文件 (`prof_attr`) 数据库

> NOTE
