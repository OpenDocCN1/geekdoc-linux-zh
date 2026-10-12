
## TABLE 19.3 Switches Used by the `AllowOverrides` Directive

| Switch | Description |
| :--- | :--- |
| `Options` | The .htaccess file can add options not listed in the Options directive for this directory. |
| `FileInfo` | The .htaccess file can include directives for modifying document type information. |
| `AuthConfig` | The .htaccess file might contain authorization directives. |
| `Limit` | The .htaccess file might contain allow, deny, and order directives. |

## File System Authentication and Access Control

You're likely to include material on your website that isn't supposed to be available to the public. You must be able to lock out this material from public access and provide designated users with the means to unlock the material. Apache provides two methods for accomplishing this type of access: authentication and authorization. You can use different criteria to control access to sections of your website, including checking the client's IP address or hostname, or requiring a username and password. This section briefly covers some of these methods.

> **CAUTION**
>
> Allowing individual users to put web content on your server poses several important security risks. If you're operating a web server on the Internet rather than on a private network, you should read the WWW Security FAQ at http://www.w3.org/Security/Faq/www-security-faq.html.

## Restricting Access with `allow` and `deny`

One of the simplest ways to limit access to website material is to restrict access to a specific group of users, based on IP addresses or hostnames. Apache uses the `allow` and `deny` directives to accomplish this.

Both directives take an address expression as a parameter. The following list provides the possible values and use of the address expression:

- `all` can be used to affect all hosts.
- A hostname or domain name, which can either be a partially or a fully qualified domain name; for example, `test.gnu.org` or `gnu.org`.
- An IP address, which can be either full or partial; for example, `12.85.67` or `12.85.67.66`.
- A network/netmask pair, such as `12.85.67.0/255.255.255.0`.
- A network address specified in classless inter-domain routing (CIDR) format; for example, `12.85.67.0/24`. This is the CIDR notation for the same network and netmask that were used in the previous example.

If you have the choice, it's preferable to base your access control on IP addresses rather than hostnames. Doing so results in faster performance because no name lookup is necessary—the IP address of the client is included with each request.

You also can use `allow` and `deny` to provide or deny access to website material based on the presence or absence of a specific environment variable. For example, the following statement denies access to a request with a context that contains an environment variable named `NOACCESS`:

`deny from env=NOACCESS`

The default behavior of Apache is to apply all the `deny` directives first and then check the `allow` directives. If you want to change this order, you can use the `order` statement. Apache might interpret this statement in three different ways:

- `Order deny,allow`—The `deny` directives are evaluated before the `allow` directives. If a host isn't specifically denied access, it is allowed to access the resource. This is the default ordering if nothing else is specified.
- `Order allow,deny`—All `allow` directives are evaluated before `deny` directives. If a host isn't specifically allowed access, it is denied access to the resource.
- `Order mutual-failure`—Only hosts that are specified in an `allow` directive and at the same time do not appear in a `deny` directive are allowed access. If a host doesn't appear in either directive, it is not granted access.

Consider this example. Suppose you want to allow only persons from within your own domain to access the `server-status` resource on your web. If your domain were named `gnulix.org`, you could add these lines to your configuration file:

```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from gnulix.org
</Location>
```

## Authentication

*Authentication* is the process of ensuring that visitors really are who they claim to be. You can configure Apache to allow access to specific areas of web content only to clients who can authenticate their identity. There are several methods of authentication in Apache; Basic Authentication is the most common (and the method discussed in this chapter).

Under Basic Authentication, Apache requires a user to supply a username and a password to access the protected resources. Apache then verifies that the user is allowed to access the resource in question. If the username is acceptable, Apache verifies the password. If the password also checks out, the user is authorized and Apache serves the request.

HTTP is a stateless protocol; each request sent to the server and each response is handled individually, and not in an intelligent fashion. Therefore, the authentication information must be included with each request. That means each request to a password-protected area is larger and therefore somewhat slower. To avoid unnecessary system use and delays, protect only those areas of your website that absolutely need protection.

To use Basic Authentication, you need a file that lists which users are allowed to access the resources. This file is composed of a plain text list containing name and password pairs. It looks very much like the /etc/passwd user file of your Linux system.

> **CAUTION**
>
> Don't use /etc/passwd as a user list for authentication. When you're using Basic Authentication, passwords and usernames are sent as base64-encoded text from the client to the server—which is just as readable as plain text. The username and password are included in each request that is sent to the server. So, anyone who might be snooping on Net traffic would be able to get this information!

To create a user file for Apache, use the htpasswd command. This is included with the Apache package. If you installed using the RPMs, it's in /usr/bin. Running htpasswd without any options produces the following output:

Usage:

```
htpasswd [-cmdps] passwordfile username
htpasswd -b[cmdps] passwordfile username password

htpasswd -n[mndps] username
htpasswd -nb[mndps] username password
```

- `-c` Create a new file.
- `-n` Don't update file; display results on stdout.
- `-m` Force MD5 encryption of the password.
- `-d` Force CRYPT encryption of the password (default).
- `-p` Do not encrypt the password (plaintext).
- `-s` Force SHA encryption of the password.
- `-b` Use the password from the command line rather than prompting for it.
- `-D` Delete the specified user.

On Windows, TPF and NetWare systems the `-m` flag is used by default. On all other systems, the `-p` flag will probably not work.

As you can see, it isn't a very difficult command to use. For example, to create a new user file named gnulixusers with a user named wsb, you need do something like this:

```
# htpasswd -c gnulixusers wsb
```

You would then be prompted for a password for the user. To add more users, you would repeat the same procedure, only omitting the -c flag.

You can also create user group files. The format of these files is similar to that of `/etc/groups`. On each line, enter the group name, followed by a colon, and then list all users, with each user separated by spaces. For example, an entry in a user group file might look like this:

```
gnulixusers: wsb pgj jp ajje nadia rkr hak
```

Now that you know how to create a user file, it's time to look at how Apache might use this to protect web resources.

To point Apache to the user file, use the `AuthUserFile` directive. `AuthUserFile` takes the file path to the user file as its parameter. If the file path isn't absolute—that is, beginning with a `/`—it's assumed that the path is relative to the `ServerRoot`. Using the `AuthGroupFile` directive, you can specify a group file in the same manner.

Next, use the `AuthType` directive to set the type of authentication to be used for this resource. Here, the type is set to `Basic`.

Now you need to decide to which realm the resource will belong. Realms are used to group different resources that will share the same users for authorization. A realm can consist of just about any string. The realm is shown in the Authentication dialog box on the user's web browser. Therefore, you should set the realm string to something informative. The realm is defined with the `AuthName` directive.

Finally, state which type of user is authorized to use the resource. You do this with the `require` directive. The three ways to use this directive are as follows:

- If you specify `valid-user` as an option, any user in the user file is allowed to access the resource (that is, provided she also enters the correct password).
- You can specify a list of users who are allowed access with the `users` option.
- You can specify a list of groups with the `group` option. Entries in the group list, as well as the user list, are separated by a space.

Returning to the `server-status` example you saw earlier, instead of letting users access the `server-status` resource based on hostname, you can require the users to be authenticated to access the resource. You can do so with the following entry in the configuration file:

```
<Location /server-status>
    SetHandler server-status
    AuthType Basic
    AuthName "Server status"
    AuthUserFile "/gnulixusers"
    Require valid-user
</Location>
```
