your content, you can simply run the developer and staging servers using that executable instead of your production server executable (httpd). After compiling a new executable, you may want to rename it to something like httpd_xx80 to ensure that you do not accidentally overwrite the production server executable with it.

To implement the cycle, follow these instructions.

+   1. Create two subdirectories in your Apache configuration directory called `staging` and `developer`, as follows:

```
```
mkdir /path/to/Apache/server/root/conf/staging
mkdir /path/to/Apache/server/root/conf/developer
```
```

![](bbox=[0.13, 0.35, 0.21, 0.41])

> Don’t forget to replace `/path/to/Apache/server/root/conf` with the actual path of your server configuration directory.

+   2. Copy all `*.conf` files to both the `staging` and `developer` subdirectories, as follows:

```
```
cp /path/to/Apache/server/root/conf/* .conf
cp /path/to/Apache/server/root/conf/staging/*
cp /path/to/Apache/server/root/conf/* .conf
cp /path/to/Apache/server/root/conf/developer/*
```
```

+   3. Modify the `httpd.conf` file in the `staging` subdirectory to listen to port 1080 instead of the default 80. You can either use the `Port` or `Listen` directive to do this. Similarly, you need to modify the `httpd.conf` in the `developer` subdirectory so that the `Port` or `Listen` directive is set to 8080.

+   4. Modify the `srm.conf` (or `httpd.conf`) files in the `staging` and `developer` subdirectories so that they point their `DocumentRoot` and `ScriptAlias` directives to the appropriate path. For example, the changes needed here for the directory structure shown in Figure 11-2 is:

```
```
DocumentRoot   "www/mycompany/staging/htdocs"
ScriptAlias    "/cgi-bin/" "www/mycompany/staging/cgi-bin/"
```
```

for the staging site configuration. For the developer site configuration file, it is:

```
```
DocumentRoot   "www/mycompany/developer/htdocs"
ScriptAlias    "/cgi-bin/" "www/mycompany/developer/cgi-bin/"
```
```

![](bbox=[0.13, 0.77, 0.21, 0.83])

> If you use a special configuration for your production server that uses absolute path information, you may have to edit the new configuration files further, for the `staging` and `developer` subdirectories.

# **Using multiple Apache server computers for the Web cycle**

If you can afford to have multiple Apache server computers (that is, one for development, one for staging, and one for production) to create the Web cycle environment, you don’t need to create special Apache configurations. You can simply install Apache on all your involved hosts, and treat one host as the developer site host, a second host as the staging site host, and the third host as the production site. Because you now have Apache servers running on three different hosts, you