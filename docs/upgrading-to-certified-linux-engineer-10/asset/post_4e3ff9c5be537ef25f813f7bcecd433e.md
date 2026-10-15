
Select whether you want to create a module for user configuration or for group configuration. You also have to enter the common name (cn) of the module.

# Figure 11-20

![](img/8279afe915b153902294b0e58311b75a_224_0.png)

A template for the user or group module is shown. You can find the listed attributes in the YaST schema file (/etc/openldap/schema/yast.schema).

To edit a value of an attribute, select a line from the list and then select Edit.

# Figure 11-21

![](img/8279afe915b153902294b0e58311b75a_224_1.png)

In the line of the attribute **susedefaulttemplate**, a template for new users or groups is specified. If you want to edit this template, select **Configure Template.**

# Figure 11-22

![](img/8279afe915b153902294b0e58311b75a_225_0.png)

In the upper frame you see a list of attributes and their values. Edit the template attribute values with **Edit.**

In the lower frame you can specify default values for attributes. Use the three buttons below as follows:

+   - **Add.** Add a new default value.
+   - **Edit.** Edit the selected default value.
+   - **Delete.** Delete the selected default value.

## Exercise 11-1 Set Up OpenLDAP with YaST

In this exercise, you set up an OpenLDAP server and client using YaST. The base DN is “dc=digitalairlines,dc=com” and the common name of the LDAP administrator is “cn=Administrator,dc=digitalairlines,dc=com” with password “novel”. TLS/SSL is not used in this exercise.

Do the following:

- Part I - Install OpenLDAP
- Part II - Setup the OpenLDAP Server
- Part III - Setup the OpenLDAP Client

- 1. From the main menu, start YaST.
- 2. Enter root password (novel) and select OK.
- 3. From the YaST Control Center, select Software > Software Management.
- 4. From the filter drop-down menu, select Search.
- 5. In the Search field, enter ldap; then select Search.
- 6. On the right, select the following packages:
  - nss_ldap
  - openldap2
  - openldap2-client
  - pam_ldap
- 7. Select Accept; then insert the requested SUSE Linux Enterprise Server 10 DVD.
- 8. When installation is complete, remove the DVD and close the YaST Control Center.

## Part II - Setup the OpenLDAP Server

- 1. Start YaST.
- 2. Start the YaST module Network Services > LDAP Server.
- 3. Select Yes to start the LDAP server.
- 4. Select Configure.
- 5. In the LDAP Server Configuration dialog select Add Database to add a database.
- 6. In the Add Database dialog enter the following information:

# Table 11-1

| Textbox | Value |
|---|---|
| Base DN | dc=digitalairlines,dc=com |
| LDAP Password | novell |
| Validate Password | novell |

- 7. Select OK.
- 8. In the left frame select Global Settings > TLS Settings. Make Sure that the option TLS Active is set to no.
- 9. Select Finish.

## Part III - Setup the OpenLDAP Client

- 1. Start the YaST module Network Services > LDAP Client.
- 2. Select Use LDAP to activate LDAP for user authentication.
- 3. Make sure that the content of Addresses of LDAP Servers is 127.0.0.1.
- 4. Make sure that the content of LDAP base DN is dc=digitalairlines,dc=com
- 5. Make sure that the option LDAP TLS/SSL is deactivated.
- 6. Select **Advanced Configuration**.
- 7. Select the **Administration Settings** tab.
- 8. Enter **cn=Administrator** in the textbox Administration DN.
- 9. Activate the option **Append Base DN**.
- 10. Activate the option **Create Default Configuration Objects**.
- 11. Activate the option **Home Directories on This Machine**.
- 12. Select **Accept**.
- 13. Select **Finish**.
- 14. When asked to enter the administrator password enter **novell**.

*(End of Exercise)*

- **transport.** Specifies the transport security strength factor.
- **tls.** Specifies the TLS security strength factor.
- **sasl.** Specifies the SASL security strength factor.
- **update_*.** Specifies the security strength factors required for directory updates.
- **simple_bind.** Specifies the security strength factor required for simple username/password authentication.

For a more detailed description, read the section about sasl-secprops in the slapd.conf manpage (man 5 slapd.conf).

**access to.** Grants access to a set of entries and/or attributes by one or more requesters.

Syntax: **access to objects [by requesters level control]**

The **objects** and the **requesters** are specified by their DNs.

As **requesters**, you can also use the asterisk for **everybody**. **self** means the owner object of the attribute. You can also specify a DN by **dn=DN** or a group by **group=DN**.

The **level** can be:

- **read** (Read access)
- **write** (Write access)
- **auth** (Authentication needed)
- **none** (No access)

Example 1:

```
access to attr=userpassword
by self write
by anonymous auth
by * none

access to *
by * read
```
