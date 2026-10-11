```
lxc file push /path/to/local/file my-debian/path/in/container/
```

To pull a file from a container:

```
lxc file pull my-debian/path/in/container/file /path/to/local/
```

# Taking and Managing Snapshots

To create a snapshot:

```
lxc snapshot my-debian snapshot1
```

To restore from a snapshot:

```
lxc restore my-debian snapshot1
```

# LXD Clustering

LXD supports clustering, allowing you to manage containers across multiple hosts: