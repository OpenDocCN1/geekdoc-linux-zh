

Sample startup files are traditionally kept in /etc/skel (Linux, Solaris, HP-UX) or /etc (all systems). AIX, always a bit different, stashes them in /etc/security. If you customize your vendor's startup file examples, /usr/local/etc/skel is a reasonable place to put the modified copies. Linux also keeps tidbits of startup files in the /etc/profile.d directory, where shells look for pointers on coloring the output of ls to make it unreadable on a dark background, or the path to Kerberos binaries.

Depending on the user's shell, /etc may contain system-wide startup files that are processed before the user's own startup files. For example, bash and sh read /etc/profile before processing ~/.profile and ~/.bash_profile. These files are a good place in which to put site-wide defaults, but bear in mind that users can override your settings in their own startup files. For details on other shells, see the man page for the shell in question.

Be sure to set a reasonable default value for umask; we suggest 077, 027, or 022, depending on the friendliness and size of your site. If you do not use individual groups, we recommend umask 077 because it gives the owner full access but the group and the rest of the world no access. See page 158 for details on umask.

The startup files and directories listed for the GNOME and KDE desktop environments are just the tip of the iceberg. gconf is a tool that stores application preferences for programs run under GNOME, much like the Windows registry.

## Setting permissions and ownerships

Now that the home directory is set up, turn it over to the user and make sure that the permissions on it are appropriate. The command

```
$ sudo chown -R newuser:newgroup ~newuser
```

should set ownerships properly. Note that you cannot use

```
$ sudo chown newuser:newgroup ~newuser/*
```

to chown the dot files because newuser would then own not only his own files but also the parent directory ".." (e.g., /home) as well. This is a common and dangerous mistake.

## Setting a mail home

It is convenient for each user to receive email on only one machine. This scheme is often implemented with an entry in the global aliases file /etc/mail/aliases or the sendmail userDB on the central mail server. See Chapter 20 for general information about email.

## Configuring roles and administrative privileges

Role-based access control (RBAC) allows system privileges to be tailored for individual users and is available on many of our example systems. RBAC is not a traditional part of the UNIX or Linux access control model, but if your site uses it, role configuration must be a part of the process of adding users. RBAC is covered in detail starting on page 108 in the Access Control and Rootly Powers chapter.

Legislation such as the Sarbanes-Oxley Act and the Gramm-Leach-Bliley Act in the United States has complicated many aspects of system administration in the corporate arena, including user management. Roles may be your only viable option for fulfilling some of the SOX/GLBA requirements.

## Final steps

To verify that a new account has been properly configured, first log out, then log in as the new user and execute the following commands:

```
$ pwd    /* To verify the home directory */
$ ls -la  /* To check owner/group of startup files */
```

You will need to notify new users of their login names and initial passwords. Many sites send this information by email, but for security reasons that's usually not a good idea. Do it in person or over the phone, unless you are adding 500 new freshmen to the campus's CS-1 machines. Then, punt the problem to the instructor! This is also a good time to point users toward additional documentation on local customs if you have any.

See Chapter 32 for more information about SOX and GLBA

See page 1227 for more information about written user contracts.

If your site requires users to sign a written policy agreement or appropriate use policy, be sure this step has been completed before releasing the account. This check will prevent oversights and strengthen the legal basis of any sanctions you might later need to impose.

Remind new users to change their passwords immediately. If you wish, you can enforce this by setting the password to expire within a short time. Another option is to have a script check up on new users and be sure their encrypted passwords in the shadow file have changed.

In an environment in which you know the users personally, it's relatively easy to keep track of who's using a system and why. If you manage a large and dynamic user base, however, you'll need a more formal way to keep track of accounts. Maintaining a database of contact information and account statuses will help you figure out who someone is and why they have an account once the act of creating the account has faded from memory.

## 7.5 ADDING USERS WITH USERADD

Each system's useradd implements the same basic procedure outlined above. However, it is configurable, and you will probably want to customize it to fit your environment. Since each system has its own idea of what you should customize, where you should implement the customizations, and what the default behavior should be, we cover these details in vendor-specific sections.

9. Because the same password can have many encrypted representations, this method verifies only that the user has reset the password, not that it has actually been changed to a different password.

