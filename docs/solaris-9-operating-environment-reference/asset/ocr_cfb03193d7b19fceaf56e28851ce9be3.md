# 1012

# passwd

If aging is sufficient, a check is made to ensure that the new password meets construction requirements. When you type the new password a second time, the two copies of the new password are compared. If the two copies are not identical, the cycle of prompting for the new password is repeated for, at most, two more times. Passwords must be constructed to meet the following requirements.

+   - Each password must have at least PASSLENGTH characters, where PASSLENGTH defined in /etc/default/passwd and is set to 6. The first eight characters are significant.

+   - Each password must contain at least two alphabetic characters and at least one numeric or special character. In this case, arabic refers to all upper- or lowercase letters.

+   - Each password must differ from the user's login name and any reverse or circular shift of that login name. For comparison purposes, an uppercase letter and its corresponding lowercase are equivalent.

+   - New passwords must differ from the old by at least three characters. For comparison purposes, an uppercase letter and its corresponding lowercase are equivalent.

If all requirements are met, by default, the passwd command consult /etc/nswitch.conf to determine which repositories to update. It searches the passwd and passwd_compat entries. The sources (repositories) associated with these entries are updated. However, the password update configurations supported are limited to the following cases. Failure to comply with the configurations prevents users from logging in the system.

+   - passwd: files
- passwd: ldap
- passwd: nis
- passwd: files plusnis
- passwd: compat (== files nis)
- passwd: compat (== files ldap)
- passwd: compat: ldap
- passwd: compat (== files plusnis)
- passwd_compat: nisplus

Network administrators who own the NIS+ password table can change any password attributes.
In the case of, superuser (anyone with real and effective UID equal to 0, id(1) and su(1)) can change any password. passwd does not prompt superuser for the old password. Superuser is not forced to comply with password or construction requirements.

Superuser can create a null password by pressing Return in response to the prompt for a new password. This differs from passwd -d because If NIS is in, effect the root master can change any password without being prompted for the NIS password and is not forced to comply with password construction requirements.

Normally, passwd with no arguments changes the password of the current user. When a user logs in and invokes su(1) to become superuser or another user, passwd changes the original user's password, not the password of the superuser or the new