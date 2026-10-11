# Table 5.1 Continued

| NNLS COMPONENT | DATA REQUIRED | DESCRIPTION |
| :--- | :--- | :--- |
| | Admin password | This parameter is the password for the admin user object you specified earlier. |
| | LDAP server IP address | This parameter is the IP address of the LDAP server that will be used to authenticate users to eDirectory. |
| | Samba Proxy user | eDirectory uses a proxy user account to assign rights to the Samba service. This allows the service to perform certain actions in the eDirectory tree. During installation, this user is automatically created and assigned the appropriate rights. |
| | | At this prompt, you specify the name you want used for the proxy user. You can use any valid user name as long as it hasn't already been used in the tree. |
| | Samba Proxy user password | This parameter is used to create a password for the Samba Proxy user. You can use any valid password. |
| | LDAP port | This parameter specifies which TCP/IP port will be used by Samba to communicate with the LDAP server. The default value is **389**. If you configured your LDAP server to use a different port number, be sure you enter it here. |
| | Secure LDAP port | This parameter specifies the secure TCP/IP port to be used by Samba to communicate with the LDAP server in your eDirectory tree. The default value is **636**. If you've configured your LDAP server to use a different secure port number, be sure you enter it here. |