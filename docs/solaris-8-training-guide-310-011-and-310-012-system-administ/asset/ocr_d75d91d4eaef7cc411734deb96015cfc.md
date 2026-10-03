In the following example, the size of swap is set to 64MB, and it is installed on c0t3d0s1:

```
filesys            c0t3d0s1 64 swap
```

In the next example, /usr is based on the selected software, and the installation program determines what disk to put it on when you specify the any value:

```
filesys            any auto /usr
```

The optional_parameters field can be one of the options listed in Table 21.12.

# TABLE 21.12

# OPTIONAL_PARAMETERS Options

| Option | Description |
|---|---|
| preserve | The file system on the specified slice is preserved. preserve can be specified only when size is existing and slice is ? |
| mount_options | One or more mount options that are added to the /etc/vfstab entry for the specified mount_pt_name. |

# install_type

install_type specifies whether to perform the initial installation option or the upgrade option on the system. install_type must be the first class file keyword in every profile.

Here's the syntax:

```
install_type [initial_install | upgrade]
```

Select either initial_install or upgrade.

Here's an example:

```
install_type initial_install
```