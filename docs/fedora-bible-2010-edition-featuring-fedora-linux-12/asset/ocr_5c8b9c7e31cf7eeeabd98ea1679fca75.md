# Table 10-1: useradd Command Options

| Option | Description |
| --- | --- |
| `-b base_dir` | Defines a base directory and is needed if you do not specify the `-d` option for the home directory. Appends the user name onto the end of the base directory to define the user's home directory. Directory must exist unless you also use the `-m` option. |
| `-c "comment"` | Provides a description of the new user account. Usually this is just the person's full name. Replace `comment` with the name of the user account. If the comment contains multiple words, use quotation marks. |
| `-d home_dir` | Sets the home directory to use for the account. The default is to name it the same as the login name and to place it beneath `/home`. Replace `home_dir` with the directory name to use. |
| `-D` | Rather than create a new account, saves the supplied information as the new default settings for any new accounts that are created. Stores defaults in the file `/etc/default/useradd`. |
| `-e expire_date` | Assigns the expiration date for the account in `MM/DD/YYYY` or `MM-DD-YYYY` format. Replace `expire_date` with the expiration date to use. This is best used with *temporary* employees who you know need the account for only a limited time. |
| `-f inactivity` | Sets the number of days after a password expires until the account is permanently disabled. Setting this to `0` disables the account immediately after the password has expired. Setting it to `-1` disables the option (not disabled), causing the password never to expire, which is the default behavior. Replace `inactivity` with the number to use. |
| `-g group` | Sets the primary group (as listed in the `/etc/group` file) that the new user will be in. Replace `group` with the group name to use. The default is to assign the user name as the group name. |
| `-G grouplist` | Adds the new user to the supplied comma-separated list of groups. |
| `-k skel_dir` | Sets the skeleton directory containing initial configuration files and login scripts that should be copied to a new user's home directory. This parameter can be used only in conjunction with the `-m` option. Replace `skel_dir` with the directory name to use. |
| `-K name=value` | Allows you to override environmental settings in `/etc/login.defs`. Pass the name of the environment variable to override as well as its value. |
| `-m` | Automatically creates the user's home directory and copies the files in the skeleton directory (`/etc/skel`) to it. |