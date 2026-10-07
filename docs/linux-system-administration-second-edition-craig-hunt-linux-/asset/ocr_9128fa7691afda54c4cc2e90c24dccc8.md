access (2) Check user's permissions for a file
chage (1) Change user password expiry information
useradd (8) Create a new user or update default new user information
userdel (8) Delete a user account and related files

You can see from this that the command you want is useradd; running man on that command produces the display shown in Listing 4.1.

# Listing 4.1: The Man Page Display for useradd

```
USERADD(8)                     USERADD(8)

NAME
       useradd  -  Create a new user or update default new user
                  information

SYNOPSIS
       useradd  [-c comment]  [-d home_dir]
                [-e expire_date]  [-f inactvie_time]
                [-g initial_group]  [-G  group[,...]]
                [-m  [-k skeleton_dir]  | -M]  [-p passwd]
                [-s shell]  [-u uid  [ -o]]  [-n]  [-r]  login

       useradd -D  [-g default_group]  [-b  default_home]
                [-f default_inactive]  [-e default_expire_date]
                [-s default_shell]

DESCRIPTION
       Creating New Users
              When invoked without the -D option, the useradd command
              creates a new user account using the values specified on
              the command line and the default values from the system.
              The new user account will be entered into the system files
              as needed, the home directory will be created, and initial
              files copied, depending on the command line options.  The
              version provided with Red Hat Linux will create a group
              for each user added to the system, unless -n option is
              given. The options which apply to the useradd command are

...The OPTIONS section has been omitted for space reasons...

NOTES
       The system administrator is responsible for placing the
       default user files in /etc/skel directory.
       This version of useradd was modified by Red Hat to suit
       Red Hat user/group convention.

CAVEATS
       You may not add a user to an NIS group.  This must be per-formed on the NIS server.

FILES
       /etc/passwd - user account information
       /etc/shadow - secure user account information
       /etc/group  - group information
       /etc/default/useradd - default information
       /etc/skel - directory containing default files

SEE ALSO
       chfn(1),  chsh(1),  crypt(3),  groupadd(8),  groupdel(8),
       groupmod(8),  passwd(1),  userdel(8),  usermod(8)
```