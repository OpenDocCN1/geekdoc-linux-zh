
## FTP Logins

If you are going to set up a user-based FTP service where each person accessing your system has a valid login name and password, then you must create an account for each user in the /etc/passwd file. If you are not allowing anonymous FTP access, do not create a generic login that anyone can use.

To set up an anonymous FTP server, you must create a login for the anonymous user ID (if one doesn't already exist; many versions of Linux have the entry already completed upon installation). This is done in the normal process of adding a user to the /etc/passwd file. The login name is whatever you want people to use when they access your system, such as anonymous or ftp. You need to select a login directory for the anonymous users that can be protected from the rest of the file system. A typical /etc/passwd entry looks like this:

```
ftp:*:400:51:Anonymous FTP access:/usr/ftp:/bin/false
```

This sets up the anonymous user with a login of ftp. The asterisk password prevents anyone gaining access to the account. The user ID number (400) is, of course, unique to the entire system. For better security, it is a good idea to create a separate group just for the anonymous FTP access (edit the /etc/group file to add a new group, then set the ftp user to that group). Only the anonymous FTP user should belong to that group because it can be used to set file permissions to restrict access and make your system more secure. The login directory in the preceding example is /usr/ftp, although you can choose any directory as long as it belongs to root (for security reasons, again). The startup program shown in the preceding example is /bin/false, which helps protect your system from access to accounts and utilities that do not have a strong password protection.

## Setting Up the Directories

As you will see in the next section, "Setting Permissions," you can try to make the entire anonymous FTP subdirectory structure a file system unto itself, with no allowance for the anonymous user to get anywhere other than /usr/ftp (or whatever directory you use for anonymous FTP access). For this reason, you need to create a mini-file system just for the anonymous FTP access which holds the usual directory names and basic files anyone logging in will need.

The process for setting up the directories that your anonymous FTP login will need is simple, requiring you to create a number of directories and copy files into them. Here's the basic procedure:

- 1. Create the bin directory (/usr/ftp/bin, for example) and copy the directory listing command `ls` that users will need to view directory and file details.
- 2. Create the etc directory (/usr/ftp/etc, for example) and copy your passwd file (/etc/passwd) and group file (/etc/group) into it. We’ll edit these files in a moment.
- 3. Create the lib directory (/usr/ftp/lib, for example) and copy the files `/lib/ld.so` and `/lib/libc.so.X` (where X is the version number of the libc file) into it. These files are used by `ls`. Do this step only if your `ls` command requires these files; most versions of Linux do not have this dependency.
- 4. Create the pub directory (/usr/ftp/pub, for example) to hold your accessible files. We’ll look at this directory in more detail in a moment.
- 5. Create the dev directory (/usr/ftp/dev, for example) and use the `mknod` command to copy the `/dev/zero` file. You need to retain the same major and minor device numbers as the `/dev/zero` file in `/dev`. This device file is used by `ld.so` (and hence `ls`). Do this step only if `ls` requires the `/lib` directory files mentioned earlier.

The copies of the /etc/passwd and /etc/group files are copied into the `/ftp/etc` directory. You should edit these files to remove all passwords and replace them with an asterisk. Remove all entries in both /etc/passwd and /etc/group, except those used by the anonymous FTP login (usually just anonymous and bin).

The `/ftp/pub` directory structure can be used to store the files you want to allow anonymous users to access. Copy them into this directory. You can create subdirectories as you need them for organizational purposes. It may be useful to create an upload directory somewhere in the `/ftp/pub` directory structure that has write permission, so that users can upload files to you only into this upload area.

> **NOTE**
>
> If you allow remote users to access your system, you may want to protect yourself legally by issuing a warning that their activities on your system may be recorded or logged. Unfortunately, in today’s world you have to take all steps necessary to prevent getting sued!

## Setting Permissions

You can use the `chroot` command to help protect your system. The `chroot` command makes the root directory appear to be something other than `/` on a file system. For example, since `chroot` is always set for the anonymous FTP login, any time anonymous users type a `cd` command, it can always be relative to their home directory. In other words, when they type `cd /bin`, they will really be changing to `/usr/ftp/bin` if the root has been set to `/usr/ftp`. This helps prevent access to any other areas of the file system than the FTP directory structure.

If you do create an upload area, you may want to set the permissions to allow execute and write, but not read (to prevent another user downloading the files someone else has uploaded).

Set all permissions for directories under `/ftp` to prevent write access by user, group, or other. Make sure the directories and files under `/ftp` are set to allow the anonymous login to read them (set their ownership and group permissions to the root login and group ID), and set only read permission. The directories will need execute and read permission to enable the anonymous users to enter them and obtain directory listings. This provides pretty good security. All directories in the `/ftp` directory structure should have the permissions set with the command:

```
chmod 555 dir_name
```

which sets read-execute permission only. The exception is the upload directory, which can have write permission as noted earlier.

## Test the System

Before you let anyone else onto your Linux FTP system, log into it yourself and try to access files you shouldn't be able to, move into directories out of the `/ftp` structure, and write files where you shouldn't be able to. This will provide a useful test of the permissions and directory structure. Spend a few minutes trying to read and write files. Make sure your system is buttoned up: If you don't, someone else will find the holes and exploit them.

It is a useful idea to set up a mailbox for the FTP administrator so users on other systems who need help or information can send mail to you. Create a mail alias such as `ftp-admin` in the file `/etc/aliases` (and run `newaliases` to make it effective).

Because this is a system administration book, a few useful tips may help you. To begin, decide what you want to store in your FTP directories and organize the structure logically. For example, if you are making available programs you have written, set up separate directories for each. A README file in each directory will help show browsers what it contains. A master README or INSTRUCTIONS file in the `/ftp` directory can help explain how your site is set up and what its contents are.

![](img/e8e6b47ac20475e23d48b4c476f5d891_830_0.png)

## A More Secure FTP

The FTP system discussed in the preceding sections, which is the basic one supplied with practically every Linux distribution, requires a bit of work to make it secure. However, it is still vulnerable to very experienced crackers. There's a better alternative if you are paranoid about your system's security: WU FTP. Developed at Washington University, WU FTP adds some extra features to the standard FTP system:

- Better control of user and group IDs
- Better tracking of uploads and downloads
- Automatic shutdown
- Automatic compression and decompression of files

If these features sound useful, you can obtain a copy of the source code of WU FTP from several sites, although the primary site is *wuarchive.wustl.edu*. Check for the file `/packages/wuarchive-ftp/wu-ftpd-X.X.tar.Z` (where *X.X* is the latest version number). You will get the source code that needs to be compiled on your Linux system.

WU FTP uses a number of environment variables to control the service, and the accompanying documentation helps you set it up properly. Setting up WU FTP is much more complex than standard FTP, and the extra security, while useful, may be unnecessary for many FTP site machines you may have set up at home or work (unless you have sensitive information).

## Protecting an Anonymous FTP System

Anonymous FTP is fast, relatively easy to use, and a huge security problem if you don't carefully set up your system. The following list summarizes a few simple steps to setting up a better anonymous FTP site:

- 1. Create a user account called **ftp**. Edit the `/etc/passwd` file manually and replace the password with an asterisk in the second field. This prevents anyone from gaining access through the **ftp** account.
- 2. If a home directory wasn't created for the **ftp** user when you created the account, set up a home directory for the **ftp** user's sole use (such as `/home/ftp`).
- 3. Set the **ftp** home directory so that the **root** user is the owner:
  ```
  chown root /usr/ftp
  ```
