The name you pass to mknod is the device filename, type is the hardware type (normally b for a block device, or c or u for a character device; but p is also valid, and creates a FIFO), and major and minor are the major and minor device numbers, respectively. A handful of options are valid and are described by the mknod man page.

Ordinarily, you’ll only use mknod if you’re an expert with device files. At the very least, you’ll need to know the device type, major number, and minor number. This information is device-dependent, so you’ll need to consult documentation on the device’s kernel driver to learn what to use.

# # Using File Permissions

Linux uses a set of file permissions, or the file’s mode, to determine how a file may be accessed. File permissions are an important part of Linux’s user security, as described further in Chapter 5. To use these features, you must understand how Linux treats file permissions and what tools the OS provides for permission manipulation.

# ## Understanding Accounts and Ownership

Chapter 5 describes Linux accounts in detail; however, file permissions interact with accounts, so before proceeding, you should understand the basics of Linux accounts. A Linux account is a set of data structures that programs and the kernel treat in a particular way in order to control access to the system. An account includes an alphanumeric username, a user ID (UID) number, a group ID (GID) number, information on the user’s default shell, and so on. When you log into a Linux computer, you provide a username, and Linux thereafter associates all actions you perform with the account that matches the username you provided. File permissions enable you to specify what accounts may access your files, as well as what files and programs you may access as a given user.

In addition to accounts, Linux supports groups, which are collections of accounts. The system administrator defines a set of users who belong to a specific group. In addition to being owned by a particular user, each file is associated with a specific group, and permissions to the file may be defined for that group. This feature can be used to define different sets of users, such as people who are working together on a specific project, in order to give them access to project-related files while keeping other users from accessing those files.

# ## Using File Access Permissions

File access permissions in Linux involve several components, which combine to determine who may access a file and in what way. These components also help you determine precisely what a file is—an ordinary data file, a program file, a subdirectory, or something else. You must understand this setup if you want to manipulate file permissions.