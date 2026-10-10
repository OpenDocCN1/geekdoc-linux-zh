This will lock the password of the specified user account, preventing them from logging in.

+   4. **Unlock a user account:**

```
sudo passwd -u username
```

This will unlock the password of the specified user account, allowing them to log in again.

+   5. **Delete a user's password:**

```
sudo passwd -d username
```

This will delete the password of the specified user account, effectively making it impossible to log in using a password.

+   6. **Expire a user's password:**

```
sudo passwd -e username
```

This will force the user to change their password the next time they log in.

# 39. mpostat: Report processors related statistics.