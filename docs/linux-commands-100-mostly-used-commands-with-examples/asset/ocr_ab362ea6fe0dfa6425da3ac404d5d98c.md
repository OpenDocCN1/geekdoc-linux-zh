The ` -p ` option allows you to set the encrypted password for the user. In this example, ` openssl passwd -1 ` generates the encrypted password for the string "mypassword."

+   5. **Create a user with a specific user ID (UID) and group ID (GID):**

```
sudo useradd -u 1001 -g 1001 customuser
```

The ` -u ` option sets the user ID, and the ` -g ` option sets the primary group ID for the user.

+   6. **Create a system user:**

```
sudo useradd -r sysuser
```

The ` -r ` option is used to create a system user, which is typically used for running system services.

+   7. **Set the expiration date for a user account:**

```
sudo useradd -e 2023-12-31 tempuser
```

The ` -e ` option sets the expiration date for the user account. In this example, the account for "tempuser" will expire on December 31, 2023.

+   8. **Display useradd command help:**