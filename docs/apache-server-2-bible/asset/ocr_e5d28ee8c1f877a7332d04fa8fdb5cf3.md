2. Run the `make install` command to install the httpd and support files in the directory you specified using the `--prefix` option.

3. Change to the installation directory and browse the directory. You should see subdirectories such `bin`, `cgi-bin`, `conf`, `htdocs`, `icons`, `include`, `lib`, and `logs`. For example, if you use `--prefix=/usr/local/apache` with the `configure` script during source tree configuration, `make install` will create the following directory structure:

```
/usr/local/apache
+---include
+---lib
+---bin
+---conf
+---htdocs
    |
    +---manual
        +---developer
        +---howto
        +---images
        +---misc
        +---mod
        +---platform
        +---programs
        +---search
        +---vhosts
    |
+---icons
    |
    +---small
+---logs
+---cgi-bin
```

The following list gives a brief description of each of the directories in the Apache directory structure:

+   ◊ include—Contains all the C header (include) files that are only needed if you develop Web applications that integrate with Apache or want to use use third-party software with Apache, which might require the header files. On a production server you can remove this directory.

+   ◊ lib—Houses the Apache Portable Run-Time (APR) library files, the files that are required for running Apache, and other support utilities such as ab.

+   ◊ bin—Contains the programs shown in Table 2-4.

+   ◊ conf—Houses the configuration files for Apache. It contains the files listed in Table 2-5.