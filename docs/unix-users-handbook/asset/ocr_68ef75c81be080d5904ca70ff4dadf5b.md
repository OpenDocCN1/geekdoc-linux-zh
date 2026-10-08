# NET GROUP

**NET GROUP** - This command displays and allows you to manipulate groups on a server. Without specifying any option, this command lists groups.

The following is a summary of the **NET GROUP** command.

```
C:\ NET GROUP /?

NET GROUP [groupname [\[COMMENT:"text
```

Some commonly used options follow:

+   * **/ADD** Add a group to a domain or a *username* to a group.
* **/DELETE** Delete a group from a domain or a *username* from a group.
* **groupname** Specify the *groupname* for the operation. With no options, the users who are part of the group are displayed. You can also use the *ADD* or *DELETE* options with the *groupname* to specify a *username* to add to the group.
* **/COMMENT:"text"** Add this comment to the *groupname*.
* **/DOMAIN** The operation will be performed on the primary domain control-