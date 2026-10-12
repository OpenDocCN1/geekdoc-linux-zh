specific instruction on password configuration for OpenLDAP, and we recommend you follow our instructions closely.

# ## Configuring the Server

If you have been using LDAP for years, you will be aware of its immense power and flexibility. On the other hand, if you are just trying LDAP for the first time, it will seem like the most broken component you could imagine. LDAP has very specific configuration requirements, is vastly lacking in graphical tools, and has a large number of acronyms to remember. On the bright side, all the hard work you put in will be worth it because, when it works, LDAP will hugely improve your networking experience.

The first step in configuring your LDAP server is to install the client and server applications. Select Add/Remove Applications, click the Details button next to Network Servers, and check `openldap-servers`. Then click the Details button next to System Tools and select `openldap-clients`. After you have installed them, close the dialog box and bring up a terminal.

Now, switch to the root user and edit `/etc/openldap/slapd.conf` in the text editor of your choice. This is the primary configuration file for `slapd`, the OpenLDAP server daemon. Scroll down until you see the lines `database`, `suffix`, and `rootdn`.

This is the most basic configuration for your LDAP system. What is the name of your server? The `dc` stands for *domain component*, which is the name of your domain as stored in DNS—for example, `example.com`. For our examples, we used `hudzilla.org`. LDAP considers each part of a domain name (separated by a period) to be a domain component, so the domain `hudzilla.org` is made up of a domain component `hudzilla` and a domain component `org`.

Change the `suffix` line to match your domain components, separated by commas. For example:

```
``` 
suffix "dc=hudzilla,dc=org"
```
```

The next line defines the `root DN`, which is another LDAP acronym meaning *distinguished name*. A `DN` is a complete descriptor of a person in your directory: her name and the domain in which she resides. For example

```
``` 
rootdn "cn=root,dc=hudzilla,dc=org"
```
```

`CN` is yet another LDAP acronym, this time meaning common name. A *common name* is just that—the name a person is usually called. Some people have several common names. Andrew Hudson is a common name, but that same user might also have the common name Andy Hudson. In our `rootdn` line, we define a complete user: common name `root` at domain `hudzilla.org`. These lines are essentially read backward. LDAP goes to `org` first, searches `org` for `hudzilla`, and then searches `hudzilla` for `root`.