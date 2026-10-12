
## Paul Hudson, Andrew Hudson, Nick Veitch

There are three entries there, again separated by empty lines. Each person has a DN that is made up of his common name (CN), organizational unit (OU), and domain components (DCs). He also has an `objectClass` definition, `inetOrgPerson`, which gives him standard attributes like an email address, a `photograph`, and a telephone number. Entities of type `inetOrgPerson` must have a CN and an SN (surname), so you will see them in this code.

Note also that each person has two common names: his actual name and a nickname. Not all LDAP clients support more than one CN, but there is no harm in having several as long as the main one comes first and is listed in the DN.

> **TIP**
>
> Having multiple key/value pairs, like multiple CNs, is one of the defining features of LDAP. In today’s interconnected world, few people can be defined using a single set of attributes because they have home phone numbers, work phone numbers, cell phone numbers, pager numbers, plus several email addresses, and potentially even a selection of offices where they hot desk. Using multiple CNs and other attributes allows you to properly record these complex scenarios.

The `jpegPhoto` attribute for the first entity has very particular syntax. Immediately after the colon you use an opening angle bracket (<) followed by a space and then the location of the person’s picture. Because the picture is local, it is prefixed with `file://`. It is in `/home/paul/paulHudson.jpg`, so the whole URL is `file:///home/paul/paulHudson.jpg`.

After you have edited the file to include the people in your organization, save it and close the editor. As root, issue these two commands.

```text
ldapadd -x -D "cn=root,dc=hzdzilla,dc=org" -f base.ldif
ldapadd -x -D "cn=root,dc=hzdzilla,dc=org" -f people.ldif
```

The `ldapadd` command is used to convert LDIF into live directory content and, most importantly, can be executed while your LDAP server is running. The `-x` parameter means to use only basic authentication, which means you need to supply the root username and password. `-w` means to prompt you for the password. `-D` lets you specify a DN for your username and, immediately after the `-D`, we specify the root DN as set earlier in `slapd.conf`. Finally, `-f` means to use the LDIF from the following file.

When you run them, you are prompted for the root password you set earlier. On entering it, you should see confirmation messages as your entries are added, like this:

```text
adding new entry "cn=Paul Hudson,ou=People,dc=hzdzilla,dc=org"
```

If you see an error such as `ldap_bind: Can't contact LDAP server (-1)`, you need to start the LDAP server by typing `service ldap start`. The most likely sources of other errors are typing errors. LDIF is a precise format, even down to its use of whitespace.

To test that the directory has been populated and that your configuration settings are correct, run this command:

```text
ldapsearch -x 'objectclass=*'
```

The `ldapsearch` command does what you might expect: It queries the LDAP directory from the command line. Again, `-x` means to use simple authentication, although in this situation you do not need to provide any credentials because you are only reading from the directory. The `objectclass=*` search specifies to return any entry of any objectClass, so the search will return all the entries in your directory.

You can amend the search to be more specific, for example

```text
ldapsearch -x 'cn=Ni*'
```

This returns all people with a common name that begins with Ni*. If you get results for your searches, you are ready to configure your clients.

> TIP
>
> OpenLDAP needs specific permissions for its files. The /var/lib/ldap directory should be owned by user *ldap* and group *ldap*, with permissions `600`. If you experience problems, try running `chmod 600 /var/lib/ldap`.

## Configuring Clients

Although Fedora comes with a selection of email clients, there is not enough room here to cover them all. So, we will discuss the two most frequently used clients: Evolution, the default, and Thunderbird. Both are powerful messaging solutions and so both work well with LDAP. Of the two, Thunderbird seems to be the easier to configure. We have had various problems with Evolution in situations where Thunderbird has worked the first time.

### Evolution

To configure Evolution for LDAP, click the arrow next to the New button and select Address Book. A new screen appears, the first option of which prompts you for the type of address book to create. Select On LDAP Servers.

For Name, just enter **Address book**, and for Server, enter the IP address of your LDAP server (or **127.0.0.1** if you are working on the server), as shown in Figure 28.1. Leave the port as 389, which is the default for slapd. Switch to the Details tab, and set Search Base to be the DN for your address book—for example, `ou=People,dc=hudzilla,dc=org`. Set Search Scope to be Sub so that Evolution will perform a comprehensive search. To finish, click Add Address Book.

![](img/2045828cf45e5632bf056f9ca99d6755_784_0.png)

**FIGURE 28.1** Configuring Evolution to use LDAP for addresses is easy for anonymous connections.

Although Evolution is now configured to use your directory, it will not use it for email address autocompletion just yet. To enable that, go to the **Tools** menu and click **Settings**. From the options that appear on the left, click **Autocompletion** and select your LDAP server from the list. Click **Close** and then create a new email message. If everything has worked, typing part of someone's name should pop up a box with LDAP matches.

## Thunderbird

Thunderbird is a little easier to configure than Evolution and tends to work better, particularly with entries that have multiple CNs. To enable autocompletion, go to the **Tools** menu, click **Options**, and then select **Composition** from the tab on the left.

Check the **Directory Server** box and click the **Edit Directories** button to its right. From the dialog box that appears, click **Add** to add a new directory. You can give it any name you want because this is merely for display purposes. As shown in Figure 28.2, set the **Hostname** field to be the IP address of your LDAP server (or `127.0.0.1` if you are working on the server). Set the **Base DN** to be the DN for your address book (for instance, `ou=People,dc=hudzilla,dc=org`), and leave the **port number** as `389`. Click **OK** three times to get back to the main interface.

![](img/2045828cf45e5632bf056f9ca99d6755_785_0.png)

**FIGURE 28.2** Thunderbird’s options are buried deeper than Evolution’s, but it allows you to download the LDAP directory for offline use.

Now, click **Write** to create a new email message, and type the first few letters of a user in the **To** box. If everything works, Thunderbird should pop up a box with LDAP matches.

## Administration

After your LDAP server and clients are set up, they require little maintenance until something changes externally. Specifically, if someone in your directory changes jobs, changes her phone number, gets married (changing her surname), quits, or so forth, you need to be able to update your directory to reflect the change.

OpenLDAP comes with a selection of tools for manipulating directories, of which you have already met ldapadd. To add to that, you can use ldapdelete for deleting entries in your directory and ldapmodify for modifying entries. Both are hard to use but come with moderate amounts of documentation in their man pages.

A much smarter option is to use phpLDAPadmin, which is a GPL LDAP administration tool that allows you to add and modify entries entirely through your web browser. You can learn more and download the product to try at http://www.phpldapadmin.com/.

## Reference

http://www.openldap.org/—The home page of the OpenLDAP project where you can download the latest version of the software and meet other users.

http://www.kingsmountain.com/ldaproadmap.shtml—A great set of links and resources across the Internet that explain various aspects of LDAP and its parent protocol, X.500.

http://ldap.perl.org/—The home of the Perl library for interacting with LDAP provides comprehensive documentation to get you started.

http://www.ldapguru.com/—A gigantic portal for LDAP administrators around the world. From forums dedicated to LDAP to jobs specifically for LDAP admins, this site could very well be all you need.

The definitive book on LDAP is LDAP System Administration (O'Reilly), ISBN: 1-565- 92491-6. It is an absolute must for the bookshelf of any Linux LDAP administrator. For more general reading, try LDAP Directories Explained (Addison-Wesley), ISBN: 0-201- 78792-X. It has a much stronger focus on Microsoft's Active Directory LDAP implementation, though.
