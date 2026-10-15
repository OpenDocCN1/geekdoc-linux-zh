# #71 Managing Apache Passwords

One terrific feature of the Apache web server is that it offers built-in support for password-protected directories, even on a shared public server. It's a great way to have private, secure, and limited-access information on your website, whether you're running a paid subscription service or you just want to ensure that family pictures are viewed only by family.

Standard configurations require that in the password-protected directory you manage a data file called .htaccess. This file specifies the security "zone" name, and more importantly, it points to a separate data file that contains the account name and password pairs that are used to validate access to the directory. Managing this file is not a problem, except that the only tool included with Apache for doing so is the primitive htpasswd program, which is run on the command line. As another option, this script, apm, one of the most complex and sophisticated scripts in this book, offers a password management tool that runs in your browser as a CGI script and lets you easily add new accounts, change the passwords on existing accounts, and delete accounts from the access list.

To get started, you will need a properly formatted .htaccess file to control access to the directory it's located within. For demonstration purposes, this file might look like this:

```
$ cat .htaccess
AuthUserFile /usr/lib/cgi-bin/.htpasswd
AuthGroupFile /dev/null
AuthName "Members Only Data Area."
AuthType Basic

<Limit GET>
require valid-user
</Limit>
```

A separate file, .htpasswd, contains all the account and password pairs. If this file doesn't yet exist, you'll need to create it. A blank one is fine: run touch .htpasswd and ensure that it's writable by the user ID that runs Apache itself (probably user nobody). Then you're ready for the script in Listing 9-7. This does also require, however, the CGI environment set up in "Running the Scripts in This Chapter" on page 201. Make sure this shell script is saved to your cgi-bin directory.

# The Code

```
#!/bin/bash

# apm--Apache Password Manager allows the administrator to easily
# add, update, or delete accounts and passwords for a subdirectory
# of a typical Apache configuration (where the config file is called
# .htaccess).
```