information of all users. There are seven fields for every user in this file.

username: password: UID: GID: GECOS: /home/ dir: shell

username:

Username is simply the pointing of a user ID UID to a name so that humans can retain it better.

password:

This field is where passwords of users used to be saved in the past, but now they are stored in a different file located at /etc/ shadow

UID:

It is a user ID, which is numeric and used to identify a user by the system at the most fundamental level

GID:

This is the primary group number of a user. We will discuss groups in a while

GECOS:

This is a field using arbitrary text, which usually is the full name of the user

/home/ dir:

This is the location of the home directory of the user where the user has their personal data and other configuration files

shell:

This is the program that runs after the user logs in. For a regular user, this will mostly be the program that gives the user the command line prompt

What is a group?

Just like users, there are names and group ID GID numbers associated with a group. Local group information can be found at /etc/ group

There are two types of groups. Primary and supplementary. Let's understand the features of each one by one.