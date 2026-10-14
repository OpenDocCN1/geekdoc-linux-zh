# /etc/apache2/conf.d/

This directory is listed as an included directory in the main apache2.conf file, which means that when Apache starts it will also include any configuration files found in this directory and add them to the overall configuration. Some administrators (such as yours truly) have in the past used this directory to store all of their virtual hosts, each separated in its own file, but Ubuntu now has a better solution, which is mentioned later in the chapter. Instead of containing virtual host entries, this directory is used for additional Apache options an administrator (or a package) might want to add separately from the core apache2.conf.

# /etc/apache2/mods-available/

It always used to be such a pain to add modules to Apache. Once the module itself was installed, you had to dig through a huge httpd.conf file and locate a possibly commented-out reference to include the module and most of the time also had to paste in some sort of IfModule logic as well just to make it load. Ubuntu offers a simpler, more modular approach. All of the modules that are available on the system are represented within this directory by .load and .conf files. The .load files contain all of the configuration necessary to load the modules into Apache, and the optional .conf files contain any extra configuration Apache may need to use the file after it is loaded. If you are wondering what modules you have available for your Apache install, you just need to glance in this directory.

# /etc/apache2/mods-enabled/

This directory operates much like the different runlevel directories in System V init, so if mods-available is like your init.d directory, this directory is like rcS.d (if you aren’t sure what I mean by that, check out my description of System V init in Chapter 2). Basically this directory contains symlinks to .load and .conf files in the mods-available directory. When Apache starts, it will scan this directory and load all of the modules referenced within. So if I wanted to enable the CGI module, for instance, I could type

```
$ sudo ln -s /etc/apache2/mod-available/cgi.load \
/etc/apache2/mods-enabled/cgi.load
```