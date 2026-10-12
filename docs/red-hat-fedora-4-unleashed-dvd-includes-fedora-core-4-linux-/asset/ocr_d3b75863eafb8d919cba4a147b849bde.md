**TABLE 19.3** Switches Used by the `AllowOverrides` Directive

| Switch | Description |
| :--- | :--- |
| `Options` | The .htaccess file can add options not listed in the Options directive for this directory. |
| `FileInfo` | The .htaccess file can include directives for modifying document type information. |
| `AuthConfig` | The .htaccess file might contain authorization directives. |
| `Limit` | The .htaccess file might contain allow, deny, and order directives. |

# File System Authentication and Access Control

You're likely to include material on your website that isn't supposed to be available to the public. You must be able to lock out this material from public access and provide des-ignated users with the means to unlock the material. Apache provides two methods for accomplishing this type of access: authentication and authorization. You can use different criteria to control access to sections of your website, including checking the client's IP address or hostname, or requiring a username and password. This section briefly covers some of these methods.

> **CAUTION**
> 
> Allowing individual users to put web content on your server poses several important security risks. If you're operating a web server on the Internet rather than on a private network, you should read the WWWW Security FAQ at http://www.w3.org/Security/Faq/www-security-faq.html.

# Restricting Access with `allow` and `deny`

One of the simplest ways to limit access to website material is to restrict access to a specific group of users, based on IP addresses or hostnames. Apache uses the `allow` and `deny` directives to accomplish this.

Both directives take an address expression as a parameter. The following list provides the possible values and use of the address expression:

+   *   `all` can be used to affect all hosts.
+   *   A hostname or domain name, which can either be a partially or a fully qualified domain name; for example, `test.gnu.org` or `gnu.org`.
+   *   An IP address, which can be either full or partial; for example, `12.85.67` or `12.85.67.66`.
+   *   A network/netmask pair, such as `12.85.67.0/255.255.255.0`.
+   *   A network address specified in classless inter-domain routing (CIDR) format; for example, `12.85.67.0/24`. This is the CIDR notation for the same network and netmask that were used in the previous example.