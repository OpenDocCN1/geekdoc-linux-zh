The a2dismod utility removes the symbolic links that a2enmod creates. You must reload Apache (page 902) after you give one or more of these commands before they will take effect.

The a2enmod and a2dismod utilities simplify Apache administration. Instead of adding or commenting out a LoadModule directive in the **httpd.conf** or **apache2.conf** file, you can use these programs to enable or disable a module. This setup enables APT or Synaptic, after it installs a package, to call **a2enmod** via a **dpkg** **postinst** script and then reload Apache so that the package is functional upon installation.

+   * a2ensite and a2dissite
+   
+   The **a2ensite** (Apache 2 enable site) and **a2dissite** (Apache 2 disable site) utilities enable and disable an Apache virtual host (page 937). These commands work similarly to the module commands described earlier. First you design a virtual host in a file in the */etc/apache2/sites-available* directory. Then you call **a2ensite** with the name of the site as an argument to create a symbolic link in the */etc/apache2/sites-enabled* directory. The **a2dissite** utility removes the symbolic link, disabling the virtual host.

# ### INCLUDE DIRECTIVES

Under Ubuntu, the primary configuration file is */etc/apache2/apache2.conf*. This file incorporates other files using Include directives (page 927):

```
$ grep 'aInclude' /etc/apache2/apache2.conf
Include /etc/apache2/mods-enabled/*.load
Include /etc/apache2/mods-enabled/*.conf
Include /etc/apache2/httpd.conf
Include /etc/apache2/ports.conf
Include /etc/apache2/conf.d/
Include /etc/apache2/sites-enabled/
```

+   * apache2.conf
+   
+   Typically, when you configure Apache, you do not make changes to **apache2.conf**; instead, you modify files that are specified in Include directives. You can also use the configuration tools described in the previous section. This setup allows updates to Apache to change **apache2.conf** without affecting the server.
+   
+   When Apache reads its configuration files, if it finds more than one occurrence of the same directive, even in an Include file, it uses the value assigned by the last directive it encounters.
+   
+   In the **apache2.conf** file, the Include directive for the **httpd.conf** file occurs after directives that set up the global environment, which includes various timeouts and limits as shown in Table 26-1. To change any of these directives, copy them to **httpd.conf** and make the changes there. You must change directives that appear after the **httpd.conf** Include directive in other Include files as explained in this section.

The Include directive for */etc/apache2/conf.d* (it includes all files in this directory) appears after the Include directive for **httpd.conf**, with only a few lines and the Include directive for */etc/apache2/ports.conf* separating them. This directory is a good place to put small configuration snippets, or break out parts of **httpd.conf** if it is growing too large.