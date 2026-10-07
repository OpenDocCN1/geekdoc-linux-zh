Status: 301 No more old stuff!
Location: http://gnulix.org/newstuff/
Content-type: text/html

```
<HTML>
<HEAD>
<TITLE>We've moved...</TITLE>
</HEAD>
<BODY>
<P>We've moved the old stuff and now you'll find it at:</P>
<A HREF="http://gnulix.org/newstuff/">New stuff</a>!.
</BODY>
</HTML>
```

# mod_auth

mod_auth uses a simple user authentication scheme, referred to as Basic authentication, which is based on storing usernames and encrypted passwords in a text file. This file looks much like Unix's /etc/passwd file, and is created with the htpasswd command. Refer to the "File System Authentication and Access Control" section earlier in this chapter for more information about this subject.

# mod_auth_anon

The mod_auth_anon module provides anonymous authentication similar to that of anonymous FTP: The module enables you to define user IDs of those who are to be handled as guest users. When a user tries to log on, she will be prompted for her email address as her password. It is possible to have Apache check the password to ensure it's a (more or less) proper email address. Basically, it ensures that there is an @ character and at least one character in the password.

# mod_auth_dbm

mod_auth_dbm uses Berkeley DB instead of text for user authentication files.

# mod_auth_digest

An extension of the basic mod_auth module; instead of sending the user information in plain text, it will be sent via the MD5 Digest Authentication process. This authentication scheme is defined in RFC 2617. Compared to using Basic authentication, this is a much more secure way of sending user data over the Internet. Unfortunately, not all browsers support this authentication scheme.