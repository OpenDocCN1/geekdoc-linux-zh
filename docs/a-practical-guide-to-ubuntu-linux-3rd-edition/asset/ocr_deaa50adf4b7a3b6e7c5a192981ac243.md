# # PUTTING YOUR CONTENT IN PLACE

Place the content you want Apache to serve in **/var/www**. As shown previously, Apache automatically displays the file named **index.html** in this directory. Give the following command to create such a page, replacing the default page:

```
```
$ sudo tee /var/www/index.html
<html><body><p>This is <i>my</i> test page.</p></body></html>
<html><body><p>This is <i>my</i> test page.</p></body></html>
CONTROL-D
```
```

The **tee** utility (page 254) copies standard input (page 243) to the file you give as its argument and to standard output (page 243). Because of this redirection, **tee** repeats each line you type after you press RETURN. After you create this file, either refresh the page on the browser (if it is still running) or start it again and point it at the server. The browser should display the page you just created.

# # CONFIGURING APACHE

This section describes configuration tools you can use to make your job easier. It also tells you where you can find many of the files you may need to work with as you set up and modify an Apache server. Most of the configuration files are in the **/etc/apache2** hierarchy.

# ## CONFIGURATION TOOLS

This section describes the utilities that manage some of the files in the **/etc/apache2** hierarchy. These utilities are part of the **apache2.2-common** package, which is installed as a dependency when you install **apache2**.

+   * **a2enmod** and **a2dismod**
+   
+   The **a2enmod** (Apache 2 enable module) and **a2dismod** (Apache 2 disable module) utilities enable and disable an Apache module. The **/etc/apache2/mods-available** directory holds files that contain LoadModule directives (page 928) and options for modules that are installed on the local system. The **/etc/apache2/mods-enabled** directory holds symbolic links to the files in **mods-available**. Apache incorporates these links into its configuration files by using Include directives (next section). The **a2enmod** utility creates symbolic links in the **mods-enabled** directory from configuration files in the **mods-available** directory. It works on files whose basename is given as its argument.

```
```
$ sudo -i
# cd /etc/apache2
# ls mods-available/userdir*
mods-available/userdir.conf  mods-available/userdir.load
# ls mods-enabled/userdir*
ls: mods-enabled/userdir*: No such file or directory
# a2enmod userdir
Enabling module userdir.
Run '/etc/init.d/apache2 restart' to activate new configuration!
# ls mods-enabled/userdir*
mods-enabled/userdir.conf  mods-enabled/userdir.load
# exit
$ (press ENTER)
```
```