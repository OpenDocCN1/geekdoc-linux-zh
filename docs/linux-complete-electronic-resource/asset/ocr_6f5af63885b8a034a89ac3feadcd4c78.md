/etc/shadow Secure user account information /etc/group-group information.

/etc/default/useradd Default information /etc/login.defs system-wide settings.

/etc/skel Directory containing default files.

# ## SEE ALSO

+   chfn(1), chsh(1), groupadd(8), groupdel(8), groupmod(8),  
+   passwd(1), userdel(8), usermod(8)

# ## AUTHOR

Julianne Frances Haugh <jf@tab.com>

# # USERDEL(8)

# ## NAME

**userdel**  Delete a user account and related files.

# ## SYNOPSIS

**userdel** [*-r*] *login*

# ## DESCRIPTION

The **userdel** command modifies the system account files, deleting all  
entries that refer to *login*. The named user must exist.

**-r**  Files in the user’s home directory will be removed along  
with the home directory itself. Files located in other file  
system will have to be searched for and deleted manually.

# ## FILES

*/etc/passwd*  User account information.

*/etc/shadow-*  Secure user account information.

*/etc/group-*  Group information.