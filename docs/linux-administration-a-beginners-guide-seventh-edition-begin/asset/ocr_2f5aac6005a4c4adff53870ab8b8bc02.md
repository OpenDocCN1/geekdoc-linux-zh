# Group ID Field (GID)

The next field in the /etc/passwd file is the group entry. It is the numerical equivalent of the primary group to which the user belongs. This field also plays an important role in determining user access privileges. It should be noted that in a primary group, a user can belong to other groups as well (more on later in the section “etc/group File”).

# GECOS

This field can store various pieces of information for a user. It can act as a placeholder for the user description, full name (first and last name), telephone number, and so on. This field is optional and as a result it is also possible to store multiple entries in this field by simply separating the different entries with comma,

> NOTE Of historical note, GECOS is an acronym for General Electric Comprehensive Operating System (now referred to as GCOS) and is a carryover from the early days of computing.

# Directory

This is the user's home directory, but can also be any location on the system. Each user who actually logs into the system needs a place for configuration files that are unique to that user. Along with configuration files, the directory (often referred to as the home directory) also stores the user's personal data as documents, music, pictures, and so on.

The home directory allows each user to work in an environment that he or she has specifically customized—without to worry about the personal preferences and customizations of other users. This applies even if multiple users are logged into the same system at the same time.

# Startup Scripts

Startup scripts are not quite part of the information stored in the users' database in Linux, but they nonetheless play an important role in determining and controlling a user's environment. The startup scripts in Linux are usually stored under the user's home directory, and the need to mention while we are still on the subject of the directory (home directory) field in the /etc/passwd file.

Linux/UNIX was built from the get-go for multiuser environments and tasks. Each user is allowed to have his or her own configuration files; thus, the system appears to be customized for each particular user (even if other people are logged in at the same time). The customization of each individual user environment is