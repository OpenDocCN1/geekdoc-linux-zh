# Listing 9-8: The apm-footer.html file used to add a section for creating new users

You'll likely want to save this script in the same directory you want to protect with passwords, although you can also put it in your cgi-bin directory as we have done. Either way, make sure you tweak the htpasswd and directory values at the beginning of the script as appropriate. You'll also need an .htaccess file that defines access permissions and an .htpasswd file that exists and is writable by the user who runs the Apache web server on your system.

When you use apm, make sure the first account you create is admin so you can use the script upon subsequent invocations! There's a special test in the code that allows you to create the admin account if .htpasswd is empty.

The result of running the apm script is shown in Figure 9-1. Notice that it not only lists each account but also offers options for adding another account, changing the password of an existing account, deleting an account, or listing all the accounts.

![](bbox=[0.1, 0.5, 0.9, 0.95])