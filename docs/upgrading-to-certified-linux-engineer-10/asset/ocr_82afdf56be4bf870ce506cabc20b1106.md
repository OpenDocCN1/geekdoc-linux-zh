The default scope is **sub**; **base** scope is almost never useful for nameservice lookups.

+   - **pam_password.** Specifies the password change protocol to use. The following protocols are supported:
+     - **clear.** Change password using an LDAPModify request, replacing the userPassword value with the new cleartext password.
+     - **clear_remove_old, nds or racf.** Change password using an LDAPModify request, first removing the userPassword value containing the old cleartext password, and then adding the userPassword value with the new cleartext password. This protocol is necessary for use with Novell NDS and IBM RACF.
+     - **crypt.** Change password using an LDAPModify request, first generating a one-way hash of the new password using crypt(3) and then replacing userPassword value with the new hashed password.
+     - **md5.** Change password using an LDAPModify request, first generating a one way hash of the new password using MD5 and then replacing userPassword value with the new hashed password.
+     - **ad.** Change password using an LDAPModify request, using the Active Directory Services Interface (ADSI) password change protocol.
+     - **exop.** Change password using the RFC 3062 password modify extended operation (only the new password is sent).
+     - **exop_send_old.** Change password using the RFC 3062 password modify extended operation (both the old and new passwords are sent). This is the preferred choice when using the PADL XAD identity server.

+   - **ssl.** Specifies whether to use SSL/TLS or not. The following values are possible:
+     - **on**