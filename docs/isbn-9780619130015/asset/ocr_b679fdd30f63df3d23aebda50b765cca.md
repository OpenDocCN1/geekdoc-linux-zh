# LESSON B

# objectives

After completing this lesson, you should be able to:

+   - Discuss the role of the system administrator
- Identify the system administrator's and the ordinary user's command prompts
- Change your personal password
- View files on your screen using the cat, more, less, head, and tail commands
- Redirect output to a file

# Roles of the System Administrator and Ordinary Users

# Understanding the Role of the UNIX System Administrator

There are two types of users on a UNIX system: the system administrator and ordinary users. As the name suggests, the **system administrator** manages the system by adding new users, deleting old accounts, and ensuring that the system performs services well and efficiently for all users. **Ordinary users** are all other users. The system administrator is also called the **superuser**, because the system administrator has unlimited permission to alter the system. UNIX grants this permission when the operating system is initially installed. The system administrator grants privileges and permissions to regular users.

The system administrator has a unique user name: **root**. The system administrator **owns** the root account, which means no one else can be assigned to that account. The password for the root account is confidential; only the system administrator and a back-up person know it. If the root's password is lost or forgotten, the system administrator uses an emergency rescue procedure to reset the password.

# The System Administrator's Command Line

While ordinary users type their commands after the $ (dollar sign) command prompt, the system administrator's prompt is the # (pound) symbol. The UNIX system generates a default setting for the command prompt for the system administrator in the following format:

```
[ root@hostname ] #
```

In the prompt, *hostname* is the name of the computer the system administrator logged on to.