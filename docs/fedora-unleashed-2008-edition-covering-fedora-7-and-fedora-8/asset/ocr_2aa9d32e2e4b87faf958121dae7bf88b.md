To point Apache to the user file, use the AuthUserFile directive. AuthUserFile takes the file path to the user file as its parameter. If the file path isn’t absolute—that is, beginning with a /—it’s assumed that the path is relative to the ServerRoot. Using the AuthGroupFile directive, you can specify a group file in the same manner.

Next, use the AuthType directive to set the type of authentication to be used for this resource. Here, the type is set to Basic.

Now you need to decide to which realm the resource belongs. Realms are used to group different resources that share the same users for authorization. A realm can consist of just about any string. The realm is shown in the Authentication dialog box on the user’s web browser. Therefore, you should set the realm string to something informative. The realm is defined with the AuthName directive.

Finally, state which type of user is authorized to use the resource. You do this with the require directive. The three ways to use this directive are as follows:

+   - If you specify valid-user as an option, any user in the user file is allowed to access the resource (that is, provided she also enters the correct password).
+   - You can specify a list of users who are allowed access with the users option.
+   - You can specify a list of groups with the group option. Entries in the group list, as well as the user list, are separated by a space.

Returning to the server-status example you saw earlier, instead of letting users access the server-status resource based on hostname, you can require the users to be authenticated to access the resource. You can do so with the following entry in the configuration file:

```
<Location /server-status>
    SetHandler server-status
    AuthType Basic
    AuthName 'Server status'
    AuthUserFile ".gnulixusers"
    Require valid-user
</Location>
```

# ## Final Words on Access Control

If you have host-based as well as user-based access protection on a resource, the default behavior of Apache is to require the requester to satisfy both controls. But assume that you want to mix host-based and user-based protection and allow access to a resource if either method succeeds. You can do so by using the satisfy directive. You can set the satisfy directive to All (this is the default) or Any. When set to All, all access control methods must be satisfied before the resource is served. If satisfy is set to Any, the resource is served if any access condition is met.