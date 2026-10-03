
This chapter also described the four databases that interact with each other to provide users with access to privileged operations:

- user_attr. Associates users and roles with authorizations and execution profiles.
- auth_attr. Defines authorizations and their attributes, and identifies the associated help file.
- prof_attr. Defines profiles, lists the profile's assigned authorizations, and identifies the associated help file.
- exec_attr. Defines the privileged operations assigned to a profile.

Now that you know more about RBAC, I recommend that you go back to Chapter 20 to review the Solaris Management Console, which provides an easy-to-use GUI for creating and assigning roles and assigning rights to the roles. You will find it much easier to use than the command-line equivalents.

The next chapter examines setting up a server to support stand-alone installations using the JumpStart utility. Using JumpStart, clients on the network look to the server for the installation of their operating system. JumpStart can be used to automate the entire software installation process.

## Apply Your Knowledge
### Exercises
### 20.1 Creating a User and a Role

Estimated Time: 20 minutes

To create a user and a role, perform the following steps:

1. Create the role named admin1, as shown here:
```
roleadd -u 2000 -g 10 -d /export/home/
admin1 -m admin1
passwd admin1
<assign a password to the role account>
```
2. Create a profile to allow the user to shut down a system.
Edit the /etc/security/prof_attr file and enter the following line:
```
Shutdown:::Permit system shutdown:
```
Save and exit the file.
3. Add the Shutdown and All profiles to the role as follows:
```
rolemod -P Shutdown,All admin1
```
4. Verify that the changes have been made to the user_attr database:
```
more /etc/user_attr
```
5. Create the user account and assign it access to the admin1 role:
```
useradd -u 3000 -g 10 -d /export/home/
trng1 -m -s /bin/ksh -R admin1 trng1
```
6. Assign a password to the new user account as follows:
```
passwd trng1
<assign a password>
```
7. Verify that the entry has been made to the passwd, shadow, and user_attr files as follows:
```
more /etc/passwd
more /etc/shadow
more /etc/user_attr
```
8. Assign commands to the Shutdown profile:
Edit the /etc/security/exec_attr file and add the following line:
```
Shutdown:suser:cmd::/usr/sbin/shutdown:uid=0
```
Save and exit the file.
9. Test the new role and user account as follows:
a. Log in as trng1.
b. List the profiles that are granted to you by typing the following:
```
roles
```
c. Use the su command to assume the role admin1:
```
su admin1
<enter the password for admin1>
```
d. List the profiles that are granted to you by typing the following:
```
profiles
```
e. Shut down the system:
```
/usr/sbin/shutdown -i 0 -g 0
```

## APPLY YOUR KNOWLEDGE
### Review Questions

1. Which two statements about the roleadd command are true?
- A. roleadd looks similar to the useradd command.
- B. roleadd uses the same default shell as the useradd command.
- C. The -A option associates an account with a profile.
- D. An account created with roleadd is the same as a normal login account.

2. Which component of RBAC associates users and roles with authorizations and profiles?
- A. user_attr
- B. prof_attr
- C. auth_attr
- D. exec_attr

3. Which component of RBAC defines the privileged operations assigned to a profile?
- A. user_attr
- B. prof_attr
- C. auth_attr
- D. exec_attr

4. In the execution attributes database, which of the following is not a valid value for the attr field?
- A. euid
- B. uid
- C. egid
- D. suid

5. After creating an RBAC role, you find that the only commands that can be executed within the role are the privileged commands that you have set up. Ordinary non-privileged commands are not available. The RBAC setup has a problem. What is the cause of this problem?
- A. The role is not associated with a correct profile.
- B. The access mechanism to the role is not initializing properly.
- C. The role's profile is not associated with the correct commands.
- D. The file identifying the privileged commands has missing entries.
- E. The role's profile is not associated with the correct authorizations.

6. Which three files does RBAC use?
- A. /etc/usr_attr
- B. /etc/user_attr
- C. /etc/security/exec_attr
- D. /etc/security/prof_attr

7. You want to enable a user to administer all user cron tables. This includes amending entries in any user's crontab. Given due care to system security, what should you do to enable the user to carry out this duty?
- A. Give the user the root password.
- B. Set the suid on the crontab command.
- C. Use RBAC to authorize the user to administer cron tables.
- D. Use RBAC to give the user an ID of root when executing the crontab command.
- E. Use the ACL mechanism to give the user RW access to each crontab table.

8. Which command(s) grants a user access to a role account?
- A. roleadd
- B. rolemod
- C. useradd
- D. usermod

9. Which option to the rolemod command appends an authorization to an existing list of authorizations?
- A. -A
- B. -P
- C. -a
- D. -o
- E. None

10. In which files are profiles defined?
- A. prof_attr
- B. user_attr
- C. exec_attr
- D. auth_attr

11. What statements are true regarding the following line:

```
Media Restore:suser:cmd:::/usr/lib/fs/ufs/ufsrestore:euid=0
```
- A. It represents a profile in the exec_attr database.
- B. Any role that has Media Restore as a profile is able to execute the ufsrestore command with an effective UID of root.
- C. It represents a profile in the prof_attr database.
- D. It represents a role definition in the user_attr database.

12. In RBAC, which of the following is a bundling mechanism for grouping authorizations and commands with special attributes?
- A. Profile
- B. Role
- C. Authorization
- D. Group

## Answers to Review Questions

1. A., B. The roleadd command looks very similar to the useradd command, and it uses the same default shell as the useradd command.

2. A. user_attr (extended user attributes database) associates users and roles with authorizations and profiles.

3. D. exec_attr (profile attributes database) defines the privileged operations assigned to a profile.

4. D. Four valid keys exist: euid, uid, egid, and gid.

5. A. If a role is not associated with a correct profile, the only commands that can be executed within the role are the privileged commands that you have set up. Ordinary non-privileged commands are unavailable.

6. B., C., D. The three files that RBAC uses are /etc/user_attr, /etc/security/exec_attr, and /etc/security/prof_attr.

7. C. To enable a user to administer all user cron tables, configure RBAC to authorize the user to administer cron tables.

8. C., D. Use the roleadd command to create a role account. Then, with the usermod command, assign the role to the user account using the -R option.

9. E. The rolemod command does not add to the existing authorizations; it replaces any existing authorization setting.

10. A., C. prof_attr (rights profile attributes database) defines profiles, lists the profile’s assigned authorizations, and identifies the associated help file. exec_attr (profile attributes database) defines the privileged operations assigned to a profile.

11. A., B. The following entry in the exec_attr database

```
Media Restore:suser:cmd:::/usr/lib/fs/ufs/ufsrestore:euid=0
```

represents a profile named Media Restore. Any role that has Media Restore as a profile can execute the ufsrestore command with an effective UID of root.

12. A. Execution profiles are bundling mechanisms for grouping authorizations and commands with special attributes.

## OBJECTIVES

The following test objective is covered in this chapter:

### Understand a JumpStart installation

- This chapter will help you to understand all the components of a JumpStart network installation. You'll learn about setting up servers and clients to support a JumpStart installation including JumpStart-related commands, configuration files, and services.

## CHAPTER 21
### JumpStart
