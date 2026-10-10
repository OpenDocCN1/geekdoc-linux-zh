extension so that if you need to get in touch with him or her, you'll have the information at your fingertips. (This field is sometimes referred to as the GECOs field.)

*home directory.* The home directory defines the default location for all the users' files and directories. This is the present working directory at the time of login.

*shell.* This is the startup program the user will run at the time of login. The shell is really a command interpreter for the commands the user issues from the command line. I recommend using the default POSIX shell (*usr/bin/sh*); but there are also three traditional, popular shells in the HP-UX environment: the C shell (*usr/bin/csh*); Bourne shell (*usr/old/bin/sh*); and Korn shell (*usr/bin/ksh*). Shell programming for the system administrator is covered in Chapter 6.

The location of the user's home directory is another important entry in the *etc/passwd* file. You have to select a location for the user's “home” directory in the file system where the user's files will be stored. With some of the advanced networking technology that exists, such as NFS, the user's home directory does not even have to be on a disk that is physically connected to the computer he or she is using! The traditional place to locate a user's home directory on an HP-UX system is the *home* directory in HP-UX 11.x.

The *home* directory is typically the most dynamic area in terms of growth. Users create and delete files in their home directory on a regular basis. This means you have to do more planning related to your user area than in more static areas, such as the root file system and application areas. You would typically load HP-UX and your applications and then perform relatively few accesses to these in terms of adding and deleting files and directories. The user area is continuously updated, making it more difficult to maintain.

# ## Assigning Users to Groups

After defining all user-related information, you need to consider groups. Groups are often overlooked in the HP-UX environment until the system administrator finds that all his or her users are in the very same group, even