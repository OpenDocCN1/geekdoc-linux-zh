# CUSTOMIZING USER INITIALIZATION FILES

When a user logs into a system, the shell initialization files determine the work environment. The shell startup scripts can be modified to set environment variables and directory paths needed by a specific user. These startup scripts are located in the user's home directory.

When you are setting up user initialization files, it might be important to allow the users to customize their own initialization files. This can be accomplished with centrally located and globally distributed user initialization files called site initialization files. These files let you continually introduce new functionality to all of the user work environments by editing one initialization file. The local initialization file, located in the user's home directory, allows user-specific configuration.

A local initialization file lets users further customize their own work environment. Site initialization files are located in the /etc directory, and can be edited only by root. They are designed to distribute site-wide changes to all user work environments. Individual user initialization files are located in each user's home directory, and can be customized by the owner of that directory. When a user logs in, the site initialization file is run first, and then the initialization file located in the user's home directory is run.

The most common customizations to shell startup scripts are environment variables. Table 5.8 describes environment and shell variables you might want to customize in a user initialization file.

> NOTE
Do not use system initialization files located in the /etc directory (/etc/profile, /etc/.login) to manage an individual user's work environment. These are site initialization files, considered to be global files, meant to be generic and used to set work environments for all users. The system will run this startup file first, and will then run the user's startup file located in the home directory.