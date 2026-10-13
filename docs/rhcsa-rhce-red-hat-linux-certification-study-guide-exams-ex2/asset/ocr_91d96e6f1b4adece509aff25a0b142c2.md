# Service Categories of SELinux Booleans

There are about 170 files in the /selinux/booleans directory. As the filenames in the /selinux/booleans directory are descriptive, you can use database filter commands like grep to help classify those booleans. Based on some of the services discussed in this book, the following would be some appropriate filtering commands:

```
$ ls /selinux/booleans | grep http
$ ls /selinux/booleans | grep ftp
$ ls /selinux/booleans | grep nfs
```

You'll explore each of these categories of booleans in more detail shortly. For a brief description of available booleans with their current status, run the semanage boolean -l command. The semanage command is part of and can be installed through the policycoreutils-python package.

# Boolean Configuration with the SELinux Management Tool

One of the benefits of GUI tools is a view of the "big picture." With the SELinux Management tool, you can review the active booleans and quickly get a sense of whether SELinux is set to allow few or many options associated with a service. As discussed in Chapter 4, you can start the SELinux Management tool in a GUI desktop environment with the system-config-selinux command. In the left-hand pane, click Boolean. It opens access to a group of booleans in the right side of the window. Note the ftp filter added in Figure 11-1. It filters the system for all booleans related to FTP.

Compare the list to the output of the ls /selinux/booleans | grep ftp command described earlier. Note the differences. Some booleans shown through the SELinux Management tool don't show up directly with a grep of the file list in the /selinux/booleans directory. In general, booleans like user_tcp_server are only tangentially related to FTP services.

There are a number of categories shown in the left pane of the SELinux Management Tool window; they are described in the following sections. Most of the focus here will be in the Boolean category, where most of SELinux policies are customized.

In some cases, the boolean is associated with a requirement for a SELinux file context. For example, the allow_httpd_anon_write boolean works only if associated files and directories are labeled with the public_content_rw_type. To set that type on, say, the /var/www/html/files directory (and subdirectories), you would run the following command:

```
# chcon -R -t public_content_rw_type /var/www/html/files
```