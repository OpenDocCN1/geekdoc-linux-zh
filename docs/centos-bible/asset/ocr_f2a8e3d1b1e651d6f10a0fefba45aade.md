The /etc/exports and /etc/fstab files for flashg are as follows:

# /etc/exports file

```
`/home/flashg zarkov,dale`
```

# /etc/fstab file

```
`zarkov:/home/zarkov /home/zarkov nfs defaults,_netdev 0 0
dale:/home/dale /home/dale nfs defaults,_netdev 0 0`
```

The /etc/exports and /etc/fstab files for zarkov are:

# /etc/exports

```
`/home/zarkov flashg,dale`
```

# /etc/fstab

```
`flashg:/home/flashg /home/flashg nfs defaults,_netdev 0 0
dale:/home/dale /home/dale nfs defaults,_netdev 0 0`
```

The /etc/exports and /etc/fstab files for dale are:

# /etc/exports

```
`/home/dale zarkov,flashg`
```

# /etc/fstab

```
`zarkov:/home/zarkov /home/zarkov nfs defaults,_netdev 0 0
flashg:/home/flashg /home/flashg nfs defaults,_netdev 0 0`
```

As you can see, each system uses NFS to mount the home directories from the other two systems. A user can travel from server to server and see exactly the same desktop on each system.

# # Providing Support to Users

Creating new user accounts is just one small administrative task among many. No single chapter can adequately discuss all the tasks that are involved in the ongoing support of users. But I share with you a few hints and procedures to ease that burden.