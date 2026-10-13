By default, the Apache server has a page that says it's running, it's Apache, and that it's time to drop in personal pages. poweredby.png is the graphic file referenced in the default index.html page.

> The pushd and popd utilities are a great boon if you want to temporarily pop to another directory, then zoom back to where you were. pushd is analogous to cd, but popd knows where you were before the current directory. Very helpful!

3. The full list of possible default filenames for a given directory can be found by searching for index.html in the configuration file. Again, we'll use the -n to get a few lines of context around the match:

```
# grep -2 index.html httpd.conf
#
<IfModule mod_dir.c>
DirectoryIndex index.html index.htm index.shtml index.php index.php4
->index.php3 index.phtml index.cgi
</IfModule>
```

This rather confusing-looking statement says that if the mod_dir module is loaded (and it is, by default), Apache should try to serve up one of, in order, the following files: index.html, index.htm, index.shtml, index.php, index.php4, index.php3, index.phtml, or index.cgi.

That last file is worth a bit more exploration: Files with a .cgi filename suffix are executable programs that are written to be compatible with the Apache Common Gateway Interface. They can be quite simple, even a shell script:

```
#!/bin/sh
echo "Content-type: text/html"
echo ""
echo "Hello world!"
```

But they can also be quite complex, hook into databases, and other sophisticated programs.

4. Table 23.1 lists some of the key settings for a Web server, all found in the httpd.conf file. The default value for the Red Hat Linux 7.2 distribution of Apache 1.3.23 is also shown. Be cautious if you diverge from the standard settings: Make sure you understand the security ramifications of some of the more obscure settings before you use them!