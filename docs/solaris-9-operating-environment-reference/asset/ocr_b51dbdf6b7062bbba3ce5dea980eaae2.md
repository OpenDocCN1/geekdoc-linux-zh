# 1014 passwd

+   -D domainname Consult the passwd.org_dir table in domainname. If you do not specify this option, the default domainname returned by nis_local_directory(3NSL) is used. This domain name is the same as that returned by domainname(1M).

+   -e Change the login shell for the files repository, this option works for superuser. Normal users can change the nis or nisplus repositories.

+   -g Change the comment (finger) information. For the files repository, this option works only for superuser. Normal users can change the nis or nisplus repositories.

+   -h Change the home directory.

+   -r Specify the repository to which an operation is applied. The supported repositories are files, nis, and nisplus.

+   -s name Show password attributes for the login name. For the nisplus repository, this option works for everyone. However, for the files repository, this option works only for superuser. It does not work at all nis repository, which does not support password aging.

# Superuser Options
Only superuser can use the following options.

+   -d Delete password for name. The login name is not prompted for password. It is only applicable to the files repository.

+   -f Force the user to change password at the next login by expiring the password for name.

+   -l Lock password entry for name.

+   -min max Set minimum field for name. The min field contains the minimum number of days between password changes for name. If min is greater than max, the user cannot change the password. With the -x option, unless max is set to -1 (aging off). In that case, min need not be set.

+   -w warn Set warn field for name. The warn field contains the number of days before the first expires and the user is warned. This option is not valid if password aging is disabled.

+   -x max Set maximum field for name. The max field contains the number of days that the password is valid for name. The aging for name is turned off immediately if max is set to -1. If it is set to 0, then the user is forced to change the password at the next login session and aging is turned off.

# Operands

+   name User login name.