![](bbox=[0.1, 0.1, 0.9, 0.15])

By default Samba will convert to lowercase the username before attempting to lookup the user in the database of local system accounts. Because UNIX usernames conventionally only contain lowercase characters, the *username-level* parameter is rarely needed.

However, passwords on UNIX systems often make use of mixed-case characters. This means that in order for a user on a Windows 9x/Me client to connect to a Samba server using clear-text authentication, the *password level* must be set to the maximum number of uppercase letters that *could* appear in a password. Note that if the Server OS uses the traditional DES version of *crypt*(), a *password level* of 8 will result in case-insensitive passwords as seen from Windows users. This will also result in longer login times because Samba has to compute the permutations of the password string and try them one by one until a match is located (or all combinations fail).

The best option to adopt is to enable support for encrypted passwords wherever Samba is used. Most attempts to apply the registry change to re-enable plaintext passwords will eventually lead to user complaints and unhappiness.

# ### 3.5 Common Errors

We all make mistakes. It is okay to make mistakes, as long as they are made in the right places and at the right time. A mistake that causes lost productivity is seldom tolerated; however, a mistake made in a developmental test lab is expected.

Here we look at common mistakes and misapprehensions that have been the subject of discussions on the Samba mailing lists. Many of these are avoidable by doing your homework before attempting a Samba implementation. Some are the result of a misunderstanding of the English language, which has many phrases that are potentially vague and may be highly confusing to those for whom English is not their native tongue.

# #### 3.5.1 What Makes Samba a Server?

To some, the nature of the Samba security mode is obvious, but entirely wrong all the same. It is assumed that *security* = server means that Samba will act as a server. Not so! This setting means that Samba will *try* to use another SMB server as its source for user authentication alone.

Samba is a server regardless of which security mode is chosen. When Samba is used outside of a domain security context, it is best to leave the security mode at the default setting. By default Samba-3 uses user-mode security.