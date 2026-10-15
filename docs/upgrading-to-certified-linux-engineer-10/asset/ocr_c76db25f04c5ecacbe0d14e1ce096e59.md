# Exercise 11-2 Set up an LDAP User Database

In this exercise, you add a user with the following information to your LDAP directory:

# Table 11-2

| Information | Value |
|---|---|
| Login | kbailey |
| Name | Kate Bailey |
| UID | 1010 |
| GID | 100 |
| Home directory | /home/kbailey |
| Login shell | /bin/bash |

You create a password ("novell") for user kbailey. In part II you enable an automatically creation of the home directory if a user logs in using ssh. In part III you login as user kbailey to test your configurations.

Do the following:

+   - Part I - Add Users to the LDAP Directory
+   - Part II - Set LDAP User Password
+   - Part III - Configure Automatically Home Directory Creation
+   - Part IV - Login as kbailey via SSH

# Part I - Add Users to the LDAP Directory

+   1. There should be some entries in the LDAP directory created by YaST. To see the content of your LDAP directory enter ldapsearch -x
+   2. Create an LDIF file by entering vi example.ldif