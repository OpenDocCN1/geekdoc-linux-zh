# Chapter 11: Setting Up and Supporting Users 479

This is where the extra directory level based on the system name comes the Rescue. With all of dexter's home directories located in /home/dexter and all of ratbert's home directories located in /home/ratbert, you can remove the danger of one system covering up the home directories of another. In fact, let's take this example one step further: Imagine a scenario in which the systems dexter, ratbert, and daffy have all portable desktops that are shared with the other systems. The /etc/fstab and /etc/exports files for each system should have the following lines added to them as indicated.

The /etc/exports and /etc/fstab files for dexter are as follows:

```
/etc/exports file
/home/dexter, daffy
/etc/fstab file
```

```
ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
daffy:/home/daffy /home/daffy nfs defaults 0 0
```

The /etc/exports and /etc/fstab files for ratbert are:

```
/etc/exports
/home/ratbert dexter, daffy
/etc/fstab
```

```
dexter:/home/dexter /home/dexter nfs defaults 0 0
daffy:/home/daffy /home/daffy nfs defaults 0 0
```

The /etc/exports and /etc/fstab files for daffy are:

```
/etc/exports
/home/daffy ratbert, dexter
/etc/fstab
```

```
ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
dexter:/home/dexter /home/dexter nfs defaults 0 0
```

As you can see, each system uses NFS to mount the home directories from the other systems. A user can travel from server to server and see exactly the same desktop on each system.

# Providing Support to Users

Creating new user accounts is just one small administrative task among many. No single chapter can adequately discuss all the tasks that are involved in the ongoing support of users. But I share with you a few hints and procedures to ease that burden.