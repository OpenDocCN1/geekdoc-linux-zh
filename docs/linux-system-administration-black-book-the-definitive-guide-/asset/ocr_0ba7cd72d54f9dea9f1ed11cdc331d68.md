+   18. Choose which of the four options—share, user, domain, or server—you want to use. If you intend mostly to have guest connections, then change this line to:
+   
+       `security = share`

+   19. The next item is:
+   
+       `; password server = <NT-Server-Name>`

+   20. If you want to assign a particular machine to handle authentications, give its NetBIOS name as the argument and uncomment the line. For example:
+   
+       `password server = DOMAINSERVER`
+   
+       Also review the **name resolve order** parameter to ensure that the Samba server knows how to resolve the NetBIOS name, unless this name is the same as its hostname. Special conditions for **password server** include:

+   - If you set the **security** parameter to **domain** earlier, then you must refer to domain controller(s) as the **password server** value(s).
+   - You can use variable substitutions in the **password server** value(s).
+   - You can list multiple servers if you separate them with commas.
+   - If you want Samba to try to find the password server itself, use an asterisk as the **password server** value. This tells the server to look in the file set by the **name resolution** parameter for the domain controller.
+   - If you set the **security** parameter to **server** earlier, then if you intend to use an NT domain controller, you need to set the users' ability to access that controller from the Samba server.

+   21. Continue to the following pair of lines:
+   
+       `; password level = 8`
+       `; username level = 8`

+   22. If you tend to have mixed-case passwords or usernames, then uncomment the appropriate line. Count in how far case might be mixed—for example, the chance of capital letters may exist only in the first three characters—and change the number listed to reflect your needs.

+   23. Proceed to this pair of lines:
+   
+       `; encrypt passwords = yes`
+       `; smb passwd file = /etc/smbpasswd`