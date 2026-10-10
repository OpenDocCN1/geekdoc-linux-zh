# **No Quota?**

If your system can not find the **quota**, then no limitation of file system usage is being applied.

Your home directory is indicated by a tilde (~), shorthand for /path_to_home/username. This same path is stored in the HOME variable, so you don't have to do anything to activate it. A simple application: switch from /var/music/albums/arno/2001 to images in your home directory using one elegant command:

```
rom:/var/music/albuns/arno/2001> cd ~ /images rom:~ /images> pwd /home/rom/images
```

Later in this chapter we will talk about the commands for managing files and directories in order to keep your home directory tidy.

# 3.2.4 The most important configuration files

As we mentioned before, most configuration files are stored in the /etc directory. Content can be viewed using the cat command, which sends text files to the standard output (usually your monitor). The syntax is straight forward:

```
cat file1 file2 ... fileN
```

In this section we try to give an overview of the most common configuration files. This is certainly not a complete list. Adding extra packages may also add extra configuration files in /etc. When reading the configuration files, you will find that they are usually quite well commented and self-explanatory. Some files also have man pages which contain extra documentation, such as **man group**.

| File | Information/service |
| --- | --- |
| aliases | Mail aliases file for use with the Sendmail and Postfix mail server. Running a mail server on each and every system has long been common use in the UNIX world, and almost every Linux distribution still comes with a Sendmail package. In this file local user names are matched with real names as they occur in E-mail addresses, or with other local addresses. |
| apache | Config files for the Apache web server. |
| bashrc | The system-wide confederation file for the Bourne Again SHell. Defines functions and aliases for all users. Other shells may have their own system-wide config files, like cshrc. |