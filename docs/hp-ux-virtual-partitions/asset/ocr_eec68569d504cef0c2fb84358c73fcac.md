Some features of a good password are:

+   - A minimum of six characters that should include special characters such as a slash (/), a dot (.), or an asterisk (*).

+   - No words should be used for a password.

+   - Don’t make the password personal such as name, address, favorite sports team, etc.

+   - Don’t use something easy to type such as 123456, or qwerty.

+   - Some people say that misspelled words are acceptable, but I don’t recommend using them. Spell-check programs that match misspelled words to correctly spelled words can be used to guess at words that might be misspelled for a password.

+   - A password generator that produces an intelligible passwords works the best.

user ID (UID). The identification number of the user. Every user on your system should have a unique UID. There are no conventions for UIDs. SAM will assign a UID for you when you add users, but you can always change this. I would recommend that you reserve UIDs less than 100 for system-level users.

group ID (GID). The identification number of the group. The members of the group and their GID are in the /etc/group file. You can change the GID assigned if you don’t like it, but you may also have to change the GID of many files. As a user creates a file, his or her UID is assigned to the file as well as the GID. This means if you change the GID well after users of the same group have created many files and directories, you may have to change the GID of all these elements. I usually save GIDs less than 10 for system groups.

optional user info. In this space, you can make entries, such as the user’s phone number or full name. SAM asks you for this information when you create a user. You can leave this blank, but if you manage a system or network with many users, you may want to add the user’s full name and