Here’s the syntax:

```
num_clients client_num
```

Here’s an example:

```
num_clients 10
```

In this example, space is allocated for 10 diskless clients.

# package

package designates whether a package should be added to or deleted from the software group that is installed on the system. add or delete indicates the action required. If you do not specify add or delete, add is set by default.

Here’s the syntax:

```
package package_name [add | delete]
```

package_name must be in the form SUNWname.

Here’s an example:

```
package SUNWxwman delete
```

In this example, SUNWxwman (X Window online man pages) is not installed on the system.

# partitioning

partitioning defines how the disks are divided into slices for file systems during the installation. If you do not specify partitioning, the default is set.

Here’s the syntax:

```
partitioning default | existing | explicit
```

The partitioning options are described in Table 21.15.