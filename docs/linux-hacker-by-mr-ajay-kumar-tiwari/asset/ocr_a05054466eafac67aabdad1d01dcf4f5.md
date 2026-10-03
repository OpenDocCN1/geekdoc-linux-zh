# Linux Hack

Ajay Kumar Tiwari

Note: Make sure to follow these best practices to create a strong password for the user.

# How to identify the default values used by useradd?

Following are the default values that will be used when an user is created.

```
# useradd -D
```

```
GROUP=100
```

```
HOME=/home
```

```
INACTIVE=-1
```

```
EXPIRE=
```

```
SHELL=/bin/bash
```

```
SKEL=/etc/skel
```

# Hack 71. Create a new group and assign to an user

Create a new developer group.

```
# groupadd developers
```

Validate that the group was created successfully.

```
# grep developer /etc/group
```

```
developers:x:511:
```

Add an user to an existing group.

You cannot use useradd to modify an existing user, as you’ll get the following error message.