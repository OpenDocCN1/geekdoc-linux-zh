By default, make looks for a file called Makefile and runs that. You may get error mes-sages or simple status messages from the compiler (assuming it can be found), and then you'll get your shell prompt back. The end result of all this is a single executable file called httpd, which is the HTTP daemon. If you tried to run the httpd program, you may get a message that a file is missing. The file httpd is complaining about is the Apache run-time configuration file (usually called httpd.conf).

# ## Editing the Configuration File

Whether you compiled the Apache daemon httpd yourself or it was supplied ready-to-go with a Linux CD-ROM, you now have to set up the configuration file which is usually called httpd.conf. Under the Apache directory there should be a subdirectory called conf. Inside this directory should be three configuration files called srm.conf-dist, access.conf-dist, and httpd.conf-dist. These files have to be copied to new file-names using these commands:

```
cp srm.conf-dist srm.conf
cp access.conf-dist access.conf
cp httpd.conf-dist httpd.conf
```

Use any ASCII editor and open httpd.conf. The httpd.conf file contains general infor-mation about your server such as which port to use, the username to run as, and so on. Most of the information will be fine the way it is, but you can customize it if you want. Next, open srm.conf which is used to set up the document tree for the home pages as well as special HTML instructions. Again, most of the settings will be fine. Finally, the access.conf file is used to set the base levels of access to the system, and you can edit that to suit your needs or leave the default values.

> **TIP**

Apache supplies three configuration files by default but it doesn't need to have three. In fact, it's often easier to do just that for convenience in customizing and configuring Apache. If you do use a single file, the file httpd.conf is the one to use. To tell Apache to ignore the access.conf and srm.conf files and place these commands in the httpd.conf file:

AccessConfig /dev/null
ResourceConfig /dev/null
Delete the two files access.conf and srm.conf from the directory.

To start httpd with the configuration files you've prepared, use this command:

```
httpd -f path/httpd.conf
```