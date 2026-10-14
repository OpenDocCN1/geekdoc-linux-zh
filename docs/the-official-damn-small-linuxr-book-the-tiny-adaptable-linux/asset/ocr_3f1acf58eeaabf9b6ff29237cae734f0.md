![](bbox=[0.12, 0.14, 0.86, 0.66])

# FIGURE 16-3 Check the security of your XAMPP server.

Before you begin more refined configuration of your XAMPP server, you can deal with these issues using tools provided with XAMPP. Start by running the following command (as root user from a Terminal window):

```
# /opt/lampp/lampp security
XAMPP: Quick security check...
XAMPP: Your XAMPP pages are NOT secured by a password.
XAMPP: Do you want to set a password? [yes] yes
XAMPP: Password: ********
XAMPP: Password (again): ********
XAMPP: Password protection active. Please use 'lampp' as user name!
XAMPP: MySQL is accessible via network.
XAMPP: Normally that's not recommended. Do you want me to turn it off?
[yes] yes
XAMPP: Turned off.
XAMPP: Stopping MySQL...
XAMPP: Starting MySQL...
XAMPP: The MySQL/phpMyAdmin user pma has no password set!!!
XAMPP: Do you want to set a password? [yes] yes
XAMPP: Password: ********
XAMPP: Password (again): ********
XAMPP: Setting new MySQL pma password.
```