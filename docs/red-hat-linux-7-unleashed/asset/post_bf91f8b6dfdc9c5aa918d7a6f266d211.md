
## Authentication and Access Control

There will be times when you have material on your Web site that is not supposed to be available for the general public. You need to be able to lock out these areas somehow and only provide the means to unlock them to the right users. There are several ways in which you can accomplish this type of access, authentication, and authorization with Apache. You can use different criteria to control access to these sections, from simply checking the client's IP address or hostname to asking for a username and password. This section briefly covers some of these methods.

### Access Restrictions with allow and deny

One of the simplest ways to provide access to a specific group of users is to restrict accesses based on IP addresses or hostnames. Apache uses the **allow** and **deny** directives to accomplish this. Both of these directives take an address expression as a parameter. See the following list for possible values and usage of the address expression:

- **all** can be used to affect all hosts.
- A host or domain name, which can either be a partially or a fully qualified domain name. For example: test.gnu.org or gnulib.org.
- An IP address, which can be either full or partial. For example: **212.85.67** or **212.85.67.66**.
- A network/netmask pair, such as **212.85.67.0/255.255.255.0**.
- A network address specified in CIDR format. For example, **212.85.67.0/24**. This is the CIDR notation for the same network and netmask that was used in the previous example.

If you have the choice, it is preferable to base your access control on IP addresses, rather than hostnames. This is faster, because no name lookups are necessary—the IP address of the client is included with each request.

There is also another way to use **allow** and **deny**. Apart from specifying a hostname or an IP address, you can also check for the existence of a specific environment variable. For example, the following statement will deny access to a request with a context that contains an environment variable named NOACCESS:

```text
deny from env=NOACCESS
```

The default behavior of Apache is to apply all the **deny** directives first and then check the **allow** directives. If you want to change this order you can use the **order** statement. There are three different ways in which Apache may interpret this statement:

- Order deny,allow—The deny directives are evaluated before allow. If a host is not specifically denied access it will be allowed to access the resource. This is the default ordering if nothing else is specified.
- Order allow,deny—All allow directives are evaluated before deny. If a host is not specifically allowed access it will be denied access to the resource.
- Order mutual-failure—Only hosts that are specified in an allow directive and at the same time do not appear in a deny directive will be allowed access. If a host does not appear in either directive it will not be granted access.

Consider this example. Suppose you only wanted to allow persons from within your own domain to access the server-status resource on your Web. If your domain were named gnuix.org you would add something along these lines in your configuration file:

```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from gnuix.org
</Location>
```

### Authentication

Authentication is the process of ensuring that visitors really are who they claim to be. By specifying that only certain users are allowed to access an area, Apache will request that the client authenticate itself before granting access. See Figure 12.1 for an example of how an authentication dialog might look if you are using the konqueror browser.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_404_0.png)

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_404_1.png)

There are several methods of authentication in Apache. We will cover the most common method: Basic authentication. Using this method a user will be required to supply a username and a password to access the protected resources. Apache will then verify that the user is allowed to access the resource in question. Should this be the case the password will be verified. If this also checks out, the user will have been authorized and the request will be served.

HTTP is a stateless protocol, therefore the authentication information must be included with each request. This means that each request to a password-protected area will be larger and therefore somewhat slower. Taking this into account, it is a good idea to protect only those areas that absolutely need it.

In order to use Basic authentication you will need a file that lists which users are allowed to access the resources. This list will consist of a plain text file containing name and password pairs. It looks very much like the user file of your Linux system—that is, `/etc/passwd`. In fact, you could actually use this as a user list for authentication. But this is a very bad idea!

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_405_0.png)

> When you are using Basic authentication, passwords and usernames are sent as base64-encoded text from the client to the server—which is just as readable as plain text. The username and password are included in each request that is sent to the server. So anyone who might be snooping on Net traffic could be able to get hold of this information!

To create a user file for Apache, use the `htpasswd` command. This is included with the Apache package and if you installed using the RPMs it will be found in `/usr/bin`. Running `htpasswd` without any options will produce the following output: `Usage:` `htpasswd [-cmdps] passwordfile username` `htpasswd -b[cmdps] passwordfile username password`

- `-c` Create a new file.
- `-m` Force MD5 encryption of the password.
- `-d` Force CRYPT encryption of the password (default).
- `-p` Do not encrypt the password (plaintext).
- `-s` Force SHA encryption of the password.
- `-b` Use the password from the command line rather than prompting for it. On Windows and TPF systems the `-m` flag is used by default. On all other systems, the `-p` flag will probably not work.

As you can see, it is not a very difficult command to use. For example, to create a new user file named `gnulixusers` with a user named `wsb` you would need to do something like this: `htpasswd -c gnulixusers wsb`

You would then be prompted for a password for the user. To add more users you would repeat the same procedure, only omitting the `-c` flag.

You can also create user group files. The format of these files is more or less like the `/etc/groups`. The first entry on a line is the group name. A colon follows this and then a list of all users is specified, separated by spaces. For example, an entry might look like this: `gnulickers: wsb pgy jp ajje nadia rkr hak`

Now that you know how to create a user file, it is time to look at how Apache might use this to protect Web resources. First of all you will want to point Apache to the user file. You do this with the AuthUserFile directive. As its parameter the directive takes the file path to the user file. If it is not absolute—that is, beginning with a /—it will be assumed that it is relative to the ServerRoot. Using the AuthGroupFile directive, you can specify a group file in the same manner.

The next directive you need to use is AuthType. This sets the type of authentication to be used for this resource. Because this section is looking at how to use Basic authentication, this will be set to Basic.

Now you need to decide what realm the resource is to belong to. This is used to group different resources that will share the same users for authorization. The realm can consist of just about any string. The realm will be shown in the Authentication dialog on the user’s Web browser. Therefore, it is best to set the realm string to something informative. The realm is defined with the AuthName directive.

Finally, you need to state what type of users are required for the resource. You do this with the require directive. There are three ways to use this directive:

- If you specify valid-user as an option, any user in the user file will be allowed to access the resource (that is, provided he or she also entered the correct password).
- You can specify a list of users who are allowed access with the users option.
- You can specify a list of groups with the group option. Entries in the group list as well as the user list are separated by a space.

Returning to the server-status example from earlier, instead of letting users access the server-status resource based on hostname, change it to require that they be authenticated. You can do this with the following entry in the configuration file:

```
<Location /server-status>
SetHandler server-status
AuthType Basic
AuthName "Server status"
AuthUserFile "/gnuixusers"
Require valid-user
</Location>
```

### Final Words on Access Control

If you have host-based as well as user-based protection on a resource, the default behavior of Apache is to require that the requester satisfy both controls. But you want to mix host-based and user-based protection and allow access to a resource if either method succeeds. You can do this using the satisfy directive. This can either be set to All (this is
