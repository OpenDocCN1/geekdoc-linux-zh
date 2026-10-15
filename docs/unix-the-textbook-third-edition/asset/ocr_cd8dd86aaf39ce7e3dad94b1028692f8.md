```
iocage update UUID|TAG
iocage upgrade UUID|TAG [release=RELEASE]
iocage version | --version
```

For more information, read the manual page for iocage. This extensive manual page gives you all of the options, subcommands, and properties that you can use with the iocage command.

# 25.2.2 Basic Usage

This section details basic iocage command usage.

All of the commands are executed as superuser.

Fetch a release: The first step with iocage on a “pristine” system (where it has never been run before) is to fetch a release. By default, iocage will attempt to fetch the host’s current release from the freebsd.org servers. Once the release is downloaded, the most recent patches are applied.

```
# iocage fetch
```

If a specific release is required, run the following. In Section 25.2.9, we fetched Release 10.2 on our PC-BSD system. Be aware that a later release of iocage may be available to you.

```
# iocage fetch release=10.2-RELEASE
```

In the case that a specific download mirror is required:

```
# iocage fetch ftphost=ftp.hostname.org
```

You can also specify an FTP directory from which to fetch the base files:

```
# iocage fetch ftpdir=/dir/
```

Creating a jail: There are three supported basic jail types: full, clone, and base jail. In addition to these three, there are two more (empty and templates). Depending on requirements, the create subcommand can be applied to create any of the three types. By default, iocage will create a fully independent jail of the current host’s release and set the TAG property to today’s date.

For example:

```
# iocage create
```

This will create a fully independent jail.

To create a lightweight jail (clone):

```
# iocage create -c
```