# Part III

# Administration

# FIGURE 11-1

Reorganize, add, and remove run-level scripts from the Service Configuration window.

![](bbox=[0.18, 0.18, 0.72, 0.5])

+   ■ Customize — With a service selected, click Customize and select the run levels at which you want the service to start.

+   ■ Start — Click a service on the list. Select Start to request the service to start immediately.

Some administrators prefer text-based commands for managing run-level scripts and for managing other system services that start automatically. The chkconfig command can be used to list whether services that run-level scripts start, as well as services that the xinitd daemon starts, are on or off. To see a list of all system services, with indications that they are on or off, type the following:

```
# chkconfig --list | less
```

You can then page through the list to see those services. If you want to view the status of an individual service, you can add the service at the end of the list option. For example, to see whether the NFS service starts in each run level, type the following:

```
# chkconfig --list nfs
nfs           0:off     1:off     2:off     3:on      4:on      5:on      6:off
```

This example shows that the NFS service is set to be on for run levels 3, 4, and 5, but that it is set to off for run levels 0, 1, 2, and 6.