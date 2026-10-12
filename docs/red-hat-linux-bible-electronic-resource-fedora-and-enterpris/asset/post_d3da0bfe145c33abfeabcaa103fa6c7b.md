
permissions of files. See the sections on controlling FTP access for further information on setting up user directories and files.

## Adding helpful information

The FTP service on your Red Hat Linux computer is set up to automatically display messages and to alert the user to the existence of README files at different times in a user's navigation of your site. When FTP is installed, however, none of these files exist. So to help the navigation of your site, you need to create these files.

## Creating README files

A README file is a standard method of providing information about the contents of a software package or, in this case, the contents of an FTP directory. Your FTP server is set up, by default, to alert users to the existence of README files when they either log in or change into a directory that contains a README file. Here are the entries in the `/etc/ftpaccess` file that make this happen:

```
readme README* login

readme README* cwd=*
```

The asterisk at the end of README indicates that any files that begin with the word README are matched (such as README.info, README-help, or README.txt). The README file is usually in plain text, so anyone can read it. Add a README file to the `/var/ftp` directory (to describe the contents of the FTP server) or to any directory where you want to describe the contents to the user who enters that directory.

Users who enter a directory containing a README file will see a message that tells them that the README file is there. They have to open the file themselves to see the contents. Here is an example of what they will see after logging in:

```
230-Please read the file README

230- it was last modified on Thu May 23 16:46:20 2002 - 0 days ago
```

## Creating message files

If you want to make sure that the users see a message when they log in or enter a particular directory, you can create `welcome.msg` and `.message` files. You can create the files using any text editor. Two entries in the `/etc/ftpaccess` file define how message files are set to be read:

```
message /welcome.msg login

message .message cwd=*
```

You can create a `welcome.msg` in the FTP user's root directory (probably `/var/ftp` for anonymous users). It should be a plain-text message. It will appear when the user first logs in to your FTP server. In each directory, you can create a `.message` file. When users enter that directory, the contents of the `.message` file are displayed. As with the `welcome.msg` file, the `.message` file should be in plain text.

## Changing FTP login greetings

When users log in to your FTP server, they see several standard greetings. You can change the greetings they see and what those greetings include by adding to your `/etc/ftpaccess` file.

### Changing the initial greeting

By default, a user who logs in to your FTP server won’t see much information. The default greeting when a user logs in to your FTP server looks something like this:

```
$ ftp maple
Connected to maple (10.0.0.11).
220 maple FTP server (Version wu-2.6.2-8) ready.
Name (maple:mike):
```

That was the full greeting. To shorten the greetings that a user sees, you can set the greeting option to brief or terse in the `/etc/ftpaccess` file as follows:

```
greet terse
```

The terse option causes a somewhat shorter output to be displayed before the login prompt. Here is an example:

```
$ ftp maple
Connected to maple (10.0.0.11).
220 FTP server ready.
Name (maple:mike):
```

### Changing the FTP server host name

Normally, your system’s host name is displayed when someone connects to your FTP service. If you want to assign a special host name that applies only to connections to your FTP server, change that name in the `/etc/ftpaccess` file. Here is an example of the line you would enter:

```
hostname ftppine
```

The next time an FTP user connects, that user will see the host name as ftppine.

### Adding a message before login

If you want to have a message appear after a user connects to your FTP service, but before the login prompt, you can do that with the banner option in the `/etc/ftpaccess` file. First, you need to create a text file that contains the message you want to print. Next, add a banner line pointing to that file (relative to your system root, not the FTP relative root). For example:

```
banner /etc/ftpbanner.msg
```

With this example, the next time a user connects to the FTP service, the contents of the `/etc/ftpbanner.msg` file are displayed after the connection message and before the login prompt appears.

## Controlling FTP access

Just because you open your computer to public access doesn’t mean that you have to let everyone abuse your computing resources. In the `/etc/ftpaccess` file, you can define exactly which directories are readable and writable. You can limit the number of users who can access your FTP server at a time. You can also set permissions or limits to your resources for individuals or groups. The following sections describe some of your options.

### Creating user classes

By setting up user classes, you create a method of assigning access to different resources to different groups of users. Any user who does not fall into a class will not have access to your FTP server. That’s why the default class includes all users with the following line:

```
class all real, guest, anonymous *
```

First decide which groups of users you want to treat separately. An effective technique is to define your local users as one class and all other users as another class. The class keyword lets you assign classes based on network address and types of user within that address (that is, real, guest, or anonymous). For example, you may want to assign one set of permissions for all users within your Internet domain and another set for everyone else. Here’s how to do that:

```
class home real, guest, anonymous 10.0.0.0/8
class world real, guest, anonymous *
```

In this example, all users who come from a host computer with an address on network number 10.0.0.0 (presumably your local network) are assigned to the “home” class. Users from other networks are assigned to the “world” class. You can use a network number or a domain name.

> **NOTE:** The /8 following the network address is a shorthand for the netmask. It indicates that the eight leftmost bits represent the network. In this example, therefore, the number 1.0 represents the network number and the next three octets represent individual host addresses.

As discussed earlier, user types defined within each class are represented by one of the following keywords:

- **real** — For users who have a login account on the local computer.
- **guest** — For users with real login accounts who are designated as guestusers or guestgroups in the `/etc/ftpaccess` file.
- **anonymous** — For anyone who logs in under the anonymous user name.

With class names assigned, you can assign limitations or permissions to any of those classes.

## Allowing uploading of incoming files

By default, anonymous users are not permitted to upload files to your FTP server. For uploading to occur, you must specifically allow uploading in the `/etc/ftpaccess` file, using the `upload` parameter. Also, specific parameters deal with whether guest and anonymous users can delete, overwrite, rename, or change permissions of files and directories. (Remember that allowing public uploading of files to your FTP server can pose a significant security risk.)

## Opening directories for uploading

You need to add information to your `/etc/ftpaccess` to enable FTP users to upload files to your Red Hat Linux system. Here are two examples of using the `upload` parameter to permit ftp users to upload files:

```
upload    /var/ftp    /incoming    yes    mike    sales    0600
upload    /var/ftp    /testdir    yes    ftp    ftp    0666
```

These examples enable you to upload files to the `/incoming` and `/testdir` directories in the anonymous user's root directory (`/var/ftp`). The permission the user has to write to the `/incoming` directory (and its subdirectories) is as the user mike and the group sales. Files are written with `0600` permission (so only mike could read and write the files). In the second example, `ftp` user and group permission are used to create the file and its read/write permissions are open (`0666`).

> **CROSS-REFERENCE:** If you don't remember what permission settings such as `0666` and `0600` mean, refer to the description of access permissions in Chapter 4. These are common options used with the `chmod` command to change access permissions.

Allowing upload permission also allows those same users the right to create directories (within the upload areas). To disallow the creation of directories, add the `nodirs` keyword at the end of an upload line (after the permission numbers). To have the ability to create directories turned on for an instance where it may be off, add the `dirs` keyword to the end of the line.

Another useful option with the `upload` parameter is the `class` option. The `class` option lets you set upload permission for a select class of users. Here is an example of using the `class` option:

```
upload class=home /var/ftp /incoming/local yes ftp guest 0666
```

In this example, along with the previous example, any anonymous user could write to the `/incoming` directory, but only those who belonged to the class called `home` can write to the `/incoming/local` directory (within the `/var/ftp` directory). The permissions in this case are open (`0666`), and files and directories are created with FTP and guest for the user and group who own the file, respectively.

Using `upload` is not enough to ensure that an anonymous user can upload files to your FTP directories. Red Hat Linux file and directory ownership also applies. For example, if the
