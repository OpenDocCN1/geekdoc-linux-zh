To change the default group for a user, use the usermod command as follows:

```
usermod -g group name or GID username
```

where *group name* or *GID* and *username* are the correct values.

For example, the following changes the default group for user myfrog to 777:

```
usermod -g 777 myfrog
```

If you are using shadow passwords, you can change the expiration date of a user account using the usermod command as follows:

```
usermod -e MM/DD/YY username
```

where *MM/DD/YY* and *username* are the correct values.

For example, the following resets the account expiration date for user kabir to 12/31/01:

```
usermod -e 12/31/01 kabir
```

If you are using shadow passwords, you can change the expiration date of a user account using the usermod command as follows:

```
usermod -e MM/DD/YY username
```

where *MM/DD/YY* and *username* are the correct values.

For example, the following resets the account expiration date for user kabir to 12/31/01:

```
usermod -e 12/31/01 kabir
```

# who

**Syntax:** who

The who command displays information about the users who are currently logged in to a system. You can use the w command for the same purpose.