
Good passwords should roll out of your fingers and be easy to type. Many people are very adept at telling what you type from the motion of your fingers. If you have to think about it, it is probably not a good password for you.

# Linux and Shadow Passwords

If you are managing a computer that is connected to the Internet and that supports several users, you should consider enabling shadow passwords in your system. Shadow passwords are installed by default as a part of the standard installation. To see if shadow passwords are currently installed on your system, try this:

```
$ ls /etc/shadow
/etc/shadow
$
```

You should have received the same response. If `ls` responds instead like this, you should install shadow password support immediately:

```
ls: /etc/shadow: No such file or directory
```

Shadow passwords protect system passwords by making the file that actually contains passwords (`/etc/shadow`) readable only by root. The `/etc/passwd` file will contain stars (`*`) where the encrypted password was previously found. This is because even though passwords are encrypted in the `/etc/passwd` file, low-end computers have become very fast and able to decrypt them in a short amount of time. In the late 1980s, it probably would have taken days or weeks to decrypt this information. With today’s technology, however, it can take only a few minutes. By making the password file readable only by root, this establishes yet another security layer around this information.

For more information on shadow passwords and how to enable them, you should take a look at your man documentation for `shadow` (section 5 of the UNIX manual, `man 5 shadow`), `pwconv`, and `pwunconv`.

# SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

Publisher: Macmillan Computer Publishing

Author(s): Manuel Ricart

ISBN: 078971826x

Publication Date: 12/22/98

Bookmark it

Search this book:

Previous Table of Contents Next

## Chapter 19

### Backups: Safeguarding Your Work

#### In This Chapter

- Media Are Just Devices
- What to Back Up
- Simple Backups
- Tape Archive: `tar`
- A Backup Strategy
- Graphical Backup Programs

Without a doubt the most important maintenance task that you can perform on any computer is a backup. Backups can be tedious tasks, but it’s usually when you have neglected to do it that you most need it! Having a backup for your data can mean the difference between an inconvenience and a catastrophe. Without a backup, you’ll have a déjà vu experience recreating the work you lose. As you might already know, that is no fun. Restoring your system from a backup can be an inconvenience, and maybe a few hours of work will be lost, but it is much different than losing work you’ve created throughout past weeks, months, or even years!

A backup might be required even for simple user errors such as deleting important files. Unlike Windows or other operating systems, under UNIX/Linux there’s no “undelete” program, Norton Undelete, or any other tool to restore deleted files. If the file is deleted, it is gone. The reason these utilities don’t exist for UNIX/Linux is the way that disk space is allocated: When you delete a file and release its storage space, this space will probably be written over next. So even if such tools existed, it is likely that they would be useless. Your only guarantee of getting a file back is to have a backup.
