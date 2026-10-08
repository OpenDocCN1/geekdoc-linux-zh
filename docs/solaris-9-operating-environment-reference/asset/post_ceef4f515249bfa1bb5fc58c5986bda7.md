
# 1014 passwd

- -D domainname Consult the passwd.org_dir table in domainname. If you do not specify this option, the default domainname returned by nis_local_directory(3NSL) is used. This domain name is the same as that returned by domainname(1M).

- -e Change the login shell for the files repository, this option works for superuser. Normal users can change the nis or nisplus repositories.

- -g Change the comment (finger) information. For the files repository, this option works only for superuser. Normal users can change the nis or nisplus repositories.

- -h Change the home directory.

- -r Specify the repository to which an operation is applied. The supported repositories are files, nis, and nisplus.

- -s name Show password attributes for the login name. For the nisplus repository, this option works for everyone. However, for the files repository, this option works only for superuser. It does not work at all nis repository, which does not support password aging.

## Superuser Options
Only superuser can use the following options.

- -d Delete password for name. The login name is not prompted for password. It is only applicable to the files repository.

- -f Force the user to change password at the next login by expiring the password for name.

- -l Lock password entry for name.

- -min max Set minimum field for name. The min field contains the minimum number of days between password changes for name. If min is greater than max, the user cannot change the password. With the -x option, unless max is set to -1 (aging off). In that case, min need not be set.

- -w warn Set warn field for name. The warn field contains the number of days before the first expires and the user is warned. This option is not valid if password aging is disabled.

- -x max Set maximum field for name. The max field contains the number of days that the password is valid for name. The aging for name is turned off immediately if max is set to -1. If it is set to 0, then the user is forced to change the password at the next login session and aging is turned off.

## Operands

- name User login name.

## Environment Variables

If any of the LC* (LC_TYPE, LC_MESSAGES, LC_TIME, LC_COLLATE, LC_NUMERIC, and LC_MONETARY) (see environ(5)) are not set in the environment, the operational behavior of passwd for each locale category is determined by the value of the LANG environment variable. If LC_ALL is set, its contents are used to override the LANG and the other LC* variables. If none of the above variables are set in the environment, the C (U.S.) locale determines how passwd behaves.

- * LC_CTYPE: Determine how passwd handles characters. When LC_TYPE is set to a valid value, passwd can display and handle text and file names containing valid characters for that locale. passwd can display and handle Extended Unix (EUC) characters in which any individual character can be 1, 2, or 3 bytes. passwd can also handle EUC characters of 1, 2, or more character widths. In the C locale, only characters from ISO 8859-1 are valid.

- * LC_MESSAGES: Determine how diagnostic and informative messages are presented. This presentation includes the language and style of the messages and the correct form of affirmative and negative responses. In the C locale, the messages are presented in the default form found in the program itself (in most cases, U.S. English).

## Exit Status

- * Success.
- Permission denied.
- Invalid combination of options.
- Unexpected failure. Password file unchanged.
- Unexpected failure. Password file(s) missing.
- Password file(s) busy. Try again later.
- Invalid argument to option.
- Aging option was disabled.

## Files

```
/etc/shadow
/etc/passwd
```
Password files.

```
/etc/shadow
```
Shadow password file.

```
/etc/shells
```
File containing a list of valid shells on the system.

# 1016

### etc/default/passwd
Default values can be set for the following flags in etc/default/passwd. For example, MAXWEEKS=26.

MAXWEEKS Maximum time period that password is valid.
MINWEEKS Minimum time period before the password can be changed.
PASSLENGTH Minimum length of password, in characters.
WARNEEKS Time period until warning of date of password's pending expiration.

## Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNWcsu |
| CIS | Enabled |

## See Also

finger(1), login(1), nisppasswd(1), nistblad(1), ypppasswd(1), domainname(1), eeprom(1), id(1), pam_mgmt(1), pvconv(1), su(1), useradd(1), userdel(1), usermod(1), pam(3PAM), crypt(3), getpwnam(3C), getspawn(3C), ns_local_directory(3NSL), login(4), nnswitch.conf(4), pam_conf(4), passwd(4), shadow(4), attributes(5), environ(5), pam_ldap(5), pam_unix(5)

# paste — Merge Corresponding or Subsequent Lines of Files

## Synopsis

```
/usr/bin/paste [-s] -d list] file...
```

## Description

Use the paste command to join files together by line, writing the output to standard output. You can use paste to create new tables by pasting together fields or columns from between 1 and 12 files. Each line of each input file is considered to be one field for the output line. By default, paste adds a Tab character as the delimiter between the contributions of each file, paste takes one or more file names as arguments, reads a line from each file, and combines the lines into a single line. If some of the files have fewer lines than others, paste simply puts in the delimiters and leaves the field empty. You can specify a dash (-) as one or more of the file names to standard input.

## Options

-d list

Unless you use a backslash character (\ in list, specify each character in list as a delimiter character. If you use a backslash character, specify it and one or more characters following it as a delimiter, as described below. These elements specify one or more delimiters to use instead of the default Tab character that replaces the newline character of each of the input lines.

When you specify the -s option:
- Do not modify the last character in file.
- Reset the delimiter to the first element of list.

When you do not specify the -s option:
- Do not modify the newline character in file.
- Reset the delimiter to the first element of list.

If a backslash character appears in list, use it and the following character as a delimiter.

## Operands

file

A path of an input file.

## Usage

paste(5) for the description of behavior of paste when encountering files greater than or equal to 12.

## Examples

The following example uses the paste command to list the files in one column, using a space character as the delimiter.

```
castle ls | paste -d" " -
```
```
085X01.DOC
085X02.DOC
085X03-1.DOC
085X042.DOC
085X08.DOC
085X09.RTF
085XD.ZIP
085XFILE.ZIP
085XINTR.ZIP
a.out
ibli
bibliography.ig
C.str
DeadLetters
examples
file
kookaburra-1
ltr
Mail
new
castle%
```

The following example lists the contents of a directory in four columns, using the default table delimiter.

```
castle ls | paste - - -
085X01.DOC      085X02.DOC      085X03-1.DOC    085X042.DOC
085X08.DOC      085X09.RTF      085XD.ZIP    085XFILE.ZIP
085XINTR.ZIP    a.out           bibliography    bibliography.ig
C.str           DeadLetters     examples        file
kookaburra-1    ltr             Mail            new
castle%
```

The following example combines lines from one file into single lines. The lines in the file are numbered to make it easier for you to see the results.

```
castle -s -d"\t" kookaburra-1
1 Kookaburra sits in the old gum tree      2 Merry king
of the bush is he.
3 Laugh, kookaburra, laugh, kookaburra      4 Gay your life
must be.
5      6 Kookaburra sits in the old gum tree
7 Eating all the gundrops he can see.      8 Stop,
kookaburra, stop, kookaburra
9 Leave some there for me.
10
11 Kookaburra sits in the old gum tree      12 Merry king
of the bush is he.
13 Laugh, kookaburra, laugh, kookaburra      14 Gay your life
must be.
15 Kookaburra sits in the old gum tree
```
