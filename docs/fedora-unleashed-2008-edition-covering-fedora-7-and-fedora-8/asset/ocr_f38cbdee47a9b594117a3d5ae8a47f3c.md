After the download finishes, yum runs the installation and a test to ensure that everything completed correctly. When yum is satisfied that everything is present and correct, you are returned to the command prompt with a freshly updated system.

This is great when you want to update your entire system, but what if you want to update only certain packages? Again, yum can easily take care of this for you. You can identify the package you want and then use yum to check for its availability by using the command shown here:

```
# yum list <package name>
```

This command asks yum to cross-reference the package name with packages registered at the repositories and let you know what is available. You can use wildcards as part of the command to find out which associated packages are available. For instance, the command

```
# yum list kde*
```

searches for any packages containing kde, which is useful if you want to selectively update packages. Use the command shown here to update a single package:

```
# yum update <package name>
```

Or use this command to update more than one package at a time:

```
# yum update <package name1> <package name2>
```

Of course, when yum is processing the required packages, it also solves any dependency issues. You will get the opportunity to see not only the packages that will be updated, but also which packages were required to satisfy dependency issues.

> **About yum**
> yum is not developed solely by Red Hat. Instead, Duke University has the honor of being the creator and maintainer of yum and its related technology. In particular, Seth Vidal has spent a lot of time and effort ensuring that yum improves in both speed and functionality. Subscribe to the yum mailing list at https://lists.dulug.duke.edu/ mailman/listinfo/yum for the latest information and updates on yum. Seth has now moved across to Red Hat and spends most of his time working on yum!

# Running yum Noninteractively

Running yum can involve dependency resolution and a number of updates, which can itself take a long time to download, especially if you are connected to the Internet via a slow connection. Even with a relatively good connection (8Mbps DSL), it can take a while to download a few hundred megabytes of packages. There is, however, an option within yum that you can use to make it run with minimal user intervention. The syntax looks like this:

```
# yum -y update
```