# Configuring a Local News Server

the authentication definition. These can be listed by using either hostnames or numeric IP addresses, along with matching wildcard characters.

You can use the res parameter to specify an authentication program that is used to authenticate the connection based on its network information. Alternatively, you can use the auth parameter to specify an authentication program that can authenticate the connection by using a user ID/password pair. If you are interested in authenticating remote news servers, you should consult the IN documentation because it is a somewhat complicated process.

The access definition defines categories of access restrictions and permissions for groups of newsreaders. The syntax of the access definition is as follows:

```
access name {
  users: identity-wildmat
  newsgroups: group-wildmat
  access: permissions
}
```

The name value must match a corresponding authentication definition. The parameters defined in the access definition apply only to the hosts defined in the corresponding authentication definition. The user's parameter limits the access rules to the specific set of users listed in the value. If the users parameter isn't present, all users apply. The newsgroups parameter defines which newsgroups the group has access to, and the access parameter defines what access privileges the group has. The privileges are defined as follows:

+   - R—Read-only access is allowed.
- P—Posting articles are allowed.
- A—Posting approved articles is allowed (using a moderator).
- N—The NEWNEWS command is allowed.
- L—The group is allowed to post to newsgroups that are set to disallow local posting.

Here is a sample readers.conf file that allows all local newsreaders to read and post articles to all newsgroups:

```
# readers.conf
auth "localhost" {
  hosts: "localhost, 127.0.0.1, 192.168.1.100, stdin
  default: "<localhost>"
}
```

```
access "localhost" {
  users: "<localhost>"
}
```

![](bbox=[0.535, 0.965, 0.555, 0.985])