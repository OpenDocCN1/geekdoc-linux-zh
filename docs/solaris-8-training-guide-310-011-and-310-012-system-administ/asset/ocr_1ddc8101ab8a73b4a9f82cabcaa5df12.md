NOTE
The following error indicates that there is not enough room in the directory to install the necessary files:

```
ERROR: Insufficient space to copy Install Boot image
152691 necessary -
69372 available.
```

You'll need to either clean up files in that file system to make more room or choose a different file system.

You'll see the following error if the target directory is not empty:

```
The target directory
/export/jumpstart is not
empty. Please choose an
empty directory or remove
all files from the specified
directory and run this
program again.
```

*continued*

The system responds with this:

```
Verifying target directory...
Calculating space required for the installation boot image
Copying Solaris_8 Tools hierarchy...
Install Server setup complete
```

If no errors are displayed, the boot server is now set up. This boot server will handle all boot requests on this subnet. A client can only boot to a boot server located on its subnet. If you have JumpStart clients on other subnets, you'll need to create a boot server on each subnet. The installation program will create a subdirectory named Solaris_8 in the <boot_dir_path> directory.

# Install Server

As explained in the previous section, the boot server and the install server are typically the same system. The exception is when the client on which Solaris 8 is to be installed is located on a different subnet than the install server, a boot server is required on that subnet.

The install server is a networked system that provides Solaris 8 CD images from which you can install Solaris 8 on another system on the network. You can create an install server by copying the images on the Solaris installation media onto the server's hard disk.

By copying these CD images to the server's hard disk, you enable a single install server to provide Solaris 8 CD images for multiple releases, including Solaris 8 CD images for different platforms. For example, a SPARC install server could provide the following:

+   - Solaris 8 Software 1 of 2 SPARC Platform Edition CD image
- Solaris 8 Software 2 of 2 SPARC Platform Edition CD image
- Solaris 8 Languages SPARC Platform Edition CD image

as well as the following:

+   - Solaris 8 Software 1 of 2 Intel Platform Edition CD image
- Solaris 8 Software 2 of 2 Intel Platform Edition CD image
- Solaris 8 Languages Intel Platform Edition CD image