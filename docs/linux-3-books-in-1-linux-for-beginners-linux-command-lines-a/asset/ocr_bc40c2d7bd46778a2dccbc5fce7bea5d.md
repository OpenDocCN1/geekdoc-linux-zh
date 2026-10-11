/etc/passwd when you do not use any other options with the command. Note that this command will not set a password for the new user and, the user will not be able to login into the Linux system until a password is set.

You can type the `useradd --help` command to get the manual for the useradd command that will give you a list of options that you can pass with this command. If you manually pass options for the useradd command, they will override the user's default properties in the /etc/passwd file.

Some parameters for a user, such as the UID and password aging policy, are picked up from the file at /etc/login.defs. This file is used only when a new user is created. Modifying this user does not affect the properties of the existing users on the system.

# usermod username

This is a command that can be used to change existing users' properties in the Linux system. You can type the command `usermod --help` to get a list of all the options that can be used with this command. Let us see these options.

| Option | Description |
| :--- | :--- |
| -c, --comment COMMENT | This option is used to add a value such as full name to the GECOS field |
| -g, --gid GROUP | The primary group of the user can be specified using this option |
| -G, --groups GROUPS | Associate one or more supplementary groups with user |
| -a, --append | The option is used with the -G option to add the user to all specified supplementary groups without removing the user from other groups |
| -d, --home HOME_DIR | The option allows you to modify a new home directory for the user |
| -m, --move-home | You can move the location of the user's home directory to a new location by using the -d option |