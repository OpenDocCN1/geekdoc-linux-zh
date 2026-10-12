
## Updating the virtual table

Updating the virtual table is much the same as updating the access file. As indicated in the definitions for the `generic-linux.mc` file, you build the virtual user table by entering the following command:

```bash
# makemap -o hash /etc/mail/virtusertable < /etc/mail/virtusertable
```

This command actually creates one or more non-text files. Typically it creates a `/etc/mail/virtusertable.db` file and a `/etc/mail/virtusertable.pag` or `/etc/virtusertable.dlf` file, but does not actually change the `/etc/mail/virtusertable` file itself.

If you would like to reverse-map local users for out-bound mail---for example, to make it easier for them to send mail using their virtual domain---then you will need to add support for the generic table to your `*.mc` file. According to the FAQ located on the main sendmail page, you should do the following:

```text
FEATURE(`generictable', `hash /etc/generictable')dnl
GENERICS_DOMAIN_FILE(`/etc/sendmail.cfg')dnl
```

You will also need to create `/etc/mail/generictable`, which is like `/etc/mail/virtusertable` except that the columns are reversed:

```text
jsmith@mydomain.com     joe@astronomy.org
```

## Debugging the Files

When testing out the latest configuration, use the following command to verify the running version of sendmail:

```bash
/usr/lib/sendmail -d0.1 -bt < /dev/null
```

If the command hangs, use a `Ctrl+C` to return to the shell prompt.

In addition, it is also useful to use the `diff` utility to compare the `sendmail.cf` file to other `sendmail.cf` files that you might be making. For example, suppose that you want to make a new `*.cf` file based upon a different configuration of your `*.mc` file. You would first back up your `/etc/sendmail.cf` file to something new such as `/etc/sendmail.cf.golden`. You could then make the changes to your `*.mc` file, run `m4`, and generate another `*.cf` file. You would copy this new file to `/etc` as `sendmail.cf`, overwriting the original.

After creating a new `sendmail.cf` file, you can use `diff` to see what differences there are between the two files, `sendmail.cf` and `sendmail.cf.golden`.

Here's an example of two almost identical files.

```text
# diff sendmail.cf sendmail.cf.golden
18c18
< ###### built by root@astronomy.org on Wed Jan 20 09:36:26 MST 2000
---
> ###### built by root@astronomy.org on Tue Jan 12 16:36:21 MST 2000
```

As you can see, the only difference between the two files is that they were built on different days. This utility is also useful for comparing the `virtusertable` and similar files located on other machines.

If you are using POP3 with sendmail, be sure to include your own computer's name in the `/etc/sendmail.cw` file. This will prevent any “we don't relay” messages.

To see what domains you are relaying, enter the following line at a shell prompt:

```bash
# echo '$=w' | /usr/lib/sendmail -bt -@0.4
```

You can also use the `|` more option to scroll through the list.

## Forwarding E-mail

If a user is no longer on the mail server, yet still receives e-mail at his or her former address, you will want to implement a `.forward` file in that account. In this manner, that user can still receive e-mail sent to his or her former address at the new location. Although you could place an entry into the `/etc/aliases` file redirecting the mail to the new address, that file entry could quickly be overlooked. Instead, insert a `.forward` file in that user's home directory as soon as his or her account is deleted, leaving the home directory intact.

Be aware that the permissions on a `.forward` file should only be writable by that user and by no one else. It is simple enough for an attacker to send that user a file and then to become that user. Privileged users such as `bin` and `root` should never have a `.forward` file but should use an entry in the `/etc/aliases` file.

The regular syntax for a `.forward` file is to place the new e-mail address on the first line. If you want that user to retain e-mail delivered to the older address as well, simply enter a backslash (`\`) followed by the older account name.

For example, to have mail sent from `jsmith`'s account on `mydomain.com` over to Joe's new e-mail address at `joes@newdomain.com` yet also retain the e-mail he received at `mydomain.com` for caching purposes, you need only place the following entries into his `.forward` file to make sure that the file is writable only by Joe:

```text
# Joe's new email address
joes@newdomain.com
\jsmith
```

Now Joe will receive e-mail at his new address, but can also check for any cached messages that are stored as well at his old address.

## Adding Extra Security to Your Program

Under the FAQs on the main sendmail page, there is a very detailed explanation of some additional security issues associated with the sendmail program. This section is an excerpt taken from their page and edited slightly for clarity.

The sendmail program often gets blamed for many problems that are actually the result of other problems, such as overly permissive modes on directories. For this reason, sendmail checks the modes on system directories and files to determine whether they can be trusted. For sendmail to run without complaining, you must execute the following commands:

```bash
# chmod go-w / /etc /etc/mail /usr /var /var/spool /var/spool/mqueue
# chown root / /etc /etc/mail /usr /var /var/spool /var/spool/mqueue
```

You will probably have to tweak these commands for your environment. For example, some systems put the spool directory into `/usr/spool` instead of `/var/spool` and use the `/etc/mail` directory for the aliases file instead of `/etc`. Under Red Hat Linux, the `/var/spool` directory is the location of `mqueue/`. If you set the `runAsUser` option in your `sendmail.cf`, the `runAsUser` will have to own the `/var/spool/mqueue` directory. As a general rule, after you have compiled sendmail, run the following command to initialize the alias database:

```bash
/usr/lib/sendmail -v -bi
```

This command might generate messages such as the following:

```text
WARNING: writable directory /etc
WARNING: writable directory /usr/spool/mqueue
```

If so, the directories listed have inappropriate write permissions and you should secure them to avoid various possible security attacks.

Beginning with sendmail 8.9.x, these checks have become more strict to prevent users from being able to access files that they would normally not be able to read. In particular, `.forward` and `:include:` files, or files that redirect incoming e-mails to an executable file, in unsafe directory paths—directory paths to which groups or the world have write permission—will no longer be allowed. Therefore, if the user `joe` has a home directory that is writable by the group `staff`, sendmail will not use Joe’s `.forward` file. You can alter this behavior, at the expense of system security, by setting the `DontBlameSendmail` option.

![](img/a0884097af3186d9b4f616aaa3f065b0_672_0.png)

For example, to allow `.forward` files in group writable directories, enter the following line of code in the `/etc/sendmail.cf` file. Usually you need only uncomment the beginning of the line and add the extra variable:

- `O DontBlameSendmail=forwardfileingroupwritabledirpath`

Or, to allow these files in both group and world writable directories, enter the following:

- `O DontBlameSendmail=forwardfileinunsafedirpath`

Items from these unsafe `.forward` and `:include:` files are marked as unsafe addresses—the items cannot make deliveries to files or programs. You can alter this behavior also via the `DontBlameSendmail` option:

- `O DontBlameSendmail=forwardfileinunsafedirpath, forward-fileinunsafedirpathsafe`

The first flag allows the `.forward` file to be read, and the second allows the items in the file to be marked as safe for file and program delivery.

![](img/a0884097af3186d9b4f616aaa3f065b0_672_1.png)

Other files affected by this strengthened security include class files, such as `Fw`, `/etc/sendmail.cw`, persistent host status files, and the files specified by the `ErrorHeader` and `HelpFile` options. Similar `DontBlameSendmail` flags are available for the class, `ErrorHeader`, and `HelpFiles`.

If you have an unsafe configuration of `forward` and `include` files, you can make it safe by finding all such files and entering the command `chmod go-w $FILE` for each. Also, enter the command `chmod go-w $DIR` for each directory in the file's path.

## Setting Up Mailing Lists

Several mailing list programs are available for use with large lists of members, but probably the most efficient is `majoromo`. The `majoromo` program handles mailing lists and requires that those who subscribe to the list authenticate their identity with a return e-mail. This is a marked improvement over other e-mail mailing list managers that do not require any sort of validation and as such allow anyone to subscribe using whatever e-mail address they wish. These older or less dynamic mailing lists other than `majoromo` can be particularly troublesome for system administrators who have users subscribe with a false or bogus e-mail address. Whenever a mailing is sent, all users who have signed up using `root@localhost` as their valid e-mail cause multiple bounces to the list. `Majoromo` bypasses this problem by forcing new subscribers to provide a valid e-mail and reply to a querying e-mail proving their identity. This way someone else cannot subscribe you to an unwanted mailing list.

The first step is to download the latest version of `majoromo` from the Internet. Here's the main URL for the official `majoromo` site:

```text
http://www.greatcircle.com/majoromo/
```

About halfway down the page you will see where to download the source code. The latest version of `majoromo` also includes RPMs that you can download and use to facilitate the install process. In other situations, you can download the source code and compile it yourself.

Once you have the code, you will want to create the binary in one directory, then install it in another. I untar and unzip the source code in my home directory, `/home/kerry`, then determine my install directory to be `/usr/local/etc/majoromo-1.95.5`.
