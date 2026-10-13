# Permission configuration

The following keywords allow you to control file/directory permission settings for users.

# chmod

Syntax: chmod yes|no typelist
Default: chmod no guest,anonymous

This keyword enables or disables the chmod command (site chmod) for user types specified in the list. For example, the default setting disables this command for both guest and anonymous users. By default, the chmod command is not available.

# delete

Syntax: delete yes|no typelist
Default: delete no guest,anonymous

This keyword enables or disables the delete (del) command for users specified in the type list. For example, the default setting disables the delete command for both guest and anonymous users.

# overwrite

Syntax: overwrite yes|no typelist
Default: overwrite no guest,anonymous

This keyword enables or disables the overwriting of files by the users specified in the typelist. For example, the default setting disables file overwriting for both guest and anonymous users.