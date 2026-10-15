
+   7. Add the user to any other facilities in use as appropriate, such as the UNIX mail system and printing.

+   8. Grant or deny access to additional system resources as appropriate, using file protections or the resources' own internal mechanisms (e.g., the /etc/ftpusers file lists those users denied access to the ftp service).

+   9. Perform any other site-specific initialization tasks.

+   10. Test the new account.

## EXERCISE 23.4

Given these 10 steps, make a table or chart of what users and groups need to be added to your system, and what their default account parameters and group memberships should be. What command can you use to identify all existing groups on the system?

### 23.3.1 Adding and Deleting a User in a Text-Based Interface on PC-BSD

The following are two simple examples of how to add a new user to PC-BSD in a text-based command line interface. The first one is an interactive session that uses the adduser command to add a single user account. The second one uses adduser in batch mode, in conjunction with a file that contains a listing of several user accounts that can be added all at one time. An abbreviated listing of the syntax of the adduser command is as follows.

## SYNTAX

```
adduser [options] [option argument(s)]
```

Purpose: The adduser utility is a shell script for adding new users. It creates passwd/group entries, a home directory, copies dotfiles and sends the new user a welcome message. It supports two modes of operation. It may be used interactively at the command line to add one user at a time, or it may be directed to get the list of new users from a file and operate in batch mode without requiring any user interaction.

## Commonly used options/features:

-   -C Interactively create the /etc/adduser.conf file, whose contents become a template for new user creation. By default, this file does not exist. But if you execute adduser -C, you will be able to interactively design the contents of this file.

-   -f filename Enter batch mode, where the contents of filename are used to create multiple user accounts. When the -f option is used, the user account information must be stored in a specific format. All empty lines or lines beginning with a # will be ignored. All other lines must contain ten fields separated by colons (:), as will be described. Command line options do not take precedence over values in the fields. Only the password field may contain a colon as part of the string.

```
name:uid:class:change:expire:gecos:home_dir:shell:password
```

name Login name. This field may not be empty.

uid Numeric login user ID. If this field is left empty, it will be automatically generated.

gid Numeric primary group ID. If this field is left empty, a group with the same name as the user name will be created and its GID will be used instead.
class Login class. This field may be left empty.
change Password ageing. This field denotes the password change date for the account. The format of this field is the same as the format of the -p argument to pw. It may be dd-mmm-yy[yy], where dd is for the day, mmm is for the month in numeric or alphabetical format (e.g., 10 or Oct), and yy[yy] is the four- or two-digit year. To denote a time relative to the current date the format is: ±n[mhdw y], where n denotes a number, followed by the minutes, hours, days, weeks, months or years after which the password must be changed. This field may be left empty to turn it off.
expire Account expiration. This field denotes the expiry date of the account. The account may not be used after the specified date. The format of this field is the same as that for password ageing. This field may be left empty to turn it off.
gecos Full name and other extra information about the user.
home_dir Home directory. If this field is left empty, it will be automatically created by appending the username to the home partition. The /nonexistent home directory is considered special and is understood to mean that no home directory is to be created for the user.
shell Login shell. This field should contain either the base name or the full path to a valid login shell.
password User password. This field should contain a plaintext string, which will be encrypted before being placed in the user database. If the password type is yes and this field is empty, it is assumed the account will have an empty password. If the password type is random and this field is not empty, its contents will be used as a password. This field will be ignored if the -w option is used with a no or none argument. Be careful not to terminate this field with a closing colon (:) because it will be treated as part of the password.

The following example illustrates how to interactively create a single user account from the command line as superuser. If you make a mistake in creating a user account, you can always remove the account immediately by using the rmuser command.

## Example 23.1: PC-BSD adduser Command for a Single User Account

```
[bob@pcbsd-1727] ~% su
password: xxx
[bob@pcbsd-1727] /usr/home/bob# adduser
Username: sarwar
Full name: Mansoor Sarwar
Uid (Leave empty for default):
Login group [bob]:
Login group is bob. Invite sarwar into other groups? []:
Login class [default]:
Shell (sh csh tcsh git-shell bash rbash nologin) [sh]:
Home directory [/home/sarwar]:
```
