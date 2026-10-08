
# SYSTEM CONFIGURATION 87

Each ID consists of exactly one line in the file /etc/passwd. Each line is subdivided into a series of colon-separated fields, each with its own meaning. The corresponding documentation can be found in the man page password(5).

```
ID:password:uid:gid:directory:shell
```

- The name of the user ID must consist of one word and not contain special characters; that is, it must be composed exclusively of letters and digits. The use of foreign language characters, such as umlauts or accented letters, may cause a variety of effects. One important aspect is that many mail systems will mangle an address which, for example, umlauts. The user ID name must be unique in the system. Common IDs are first or second names in lower case letters, or nicknames. Some organizations employ numerical or other structured IDs.

- During creation of a new user ID, this field, which contains the encrypted password, should initially remain empty. Using the root login, the password can be initialized with the password ID command. If a user ID is to be created where no login will be allowed, an asterisk (*) can be used instead of the encrypted password. When shadow passwords are used, the password is not stored here, but in the file /etc/shadow. In order to prevent security problems, an asterisk (*) should be entered in any case. The password is encrypted with the libc crypt() function code is freely available. Passwords should not contain any foreign language special characters.

- The uid number (user identification) is the unique ID of a user who is also used by the kernel to check the access rights. The entries in the /etc/passwd file should be sorted in ascending order by this number, so that the useradd program can automatically find the next available number.

- The gid number (group identification) specifies the membership of a user in a user group. This makes it possible for a group of users to work on files together or allows individual users to use specific programs.

- The name should be the full (real) name of the user. This is sensible for programs such as finger, but also for the use of mail and news program. The name entered here can be changed by means of the chfn program. This field, which is also known as the gecos, can also accommodate office and private phone numbers.

# 88 CONFIGURATION AND ADMINISTRATION

Each user is associated with a home directory which becomes the current directory when the user logs in the system. This directory should be executable for all other users so that, for example, the finger daemon can change into this directory. Only the owner, however, should have write access. If the user wishes to protect data against others, then files should be stored in subdirectories of the home directory for which the corresponding access rights are set. If this directory does not exist, the user is assigned the directory as the home directory or the login is not executed, depending on the login used.

After successful login to the system, the shell can be changed by every user by means of the csh program. However, only shells are allowed that are listed in the file /etc/shells. The shell should exist, otherwise no further login is possible. This is particularly awkward if the system administrator has no valid shell. A valid shell is also required for access via ftp (see also Section 17.2).

```
root:4iEEz9nkoE:0:0:system administrator:/root:/bin/bash
uucp:*5:5:::/uucp:
jochen:EgirRB,hB4:100:Jochén Hein:/home/jochen:/bin/tcsh
guest:t401:14:account:/home/guest:/bin/tcsh
nbody:*655x4:65534:Nobody:::/bin/false
```

Listing 4.7 Example of a password file.

Listing 4.7 shows an excerpt of a password file. The system administrator root has a password and is always assigned user and group 0. This number is used by the kernel for access rights, and the value 0 as the user identification means superuser privileges. Under Unix no further subdivision of administrator rights is possible. POSIX.le is, among others, supposed to define a standard for the above; more about this subject can be found in Section 4.4.2.

/root is used as the home directory, and the bash is used as the shell. The home directory should in any case lie in the root partition to allow the user root to log in and work in single-user mode. When you change the shell of the user root, make sure that you can log back with the new shell, before you completely log out.

The second line contains a user for uucp. For this user, an asterisk (*) was registered as the password, thus logging in to the system with this ID is not possible. Such an ID is used for administration of a UUCP installation. The system administrator uses the su - uucp command to change to this user ID

# SYSTEM CONFIGURATION 89

before starting to carry out modifications to the configuration files of the UUCP system. The user jochen has a unique, non-zero user number and is a member of group 6. In the file /etc/group shown in Listing 4.14, this group number is associated with the denomination users. This association is not standardized (this may change with the LINUX Standard Base). In a network in which you use NFS, the files /etc/passwd and /etc/group should as far as possible match between the different computers. The easiest way to achieve this is by means of NIS, the Network Information System. More on this subject can be found in Chapter 21.

In the last line, you will find a guest access which is not protected by a password. This kind of access is sensible only in special cases, since it allows... (text continues based on source flow)

[Note: The provided OCR text contains significant repetitions and fragments in the latter half. I have merged the logical segments provided in the prompt.]
