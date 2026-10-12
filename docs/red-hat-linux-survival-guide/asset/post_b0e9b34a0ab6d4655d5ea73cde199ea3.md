
pretty good at increasing the number of child processes as needed based on load. So, changing this is not required.

## MaxClients

In the default-threaded MPM mode, the total number of simultaneous requests that Apache can process is MaxClients x ThreadsPerChild. So, the default maximum for simultaneous requests is 8 x 25 = 200 (you can see the default settings for these directives in the “<IfModule> containers” section earlier in the chapter). If you use the preforking MPM mode, the maximum request is limited to MaxClients. The default maximum of 200 simultaneous requests should work well for most sites, so you can leave the defaults alone.

## MinSpareThreads

The MinSpareThreads directive specifies the minimum number of idle threads; leave the default (5) as is.

## MaxSpareThreads

The MaxSpareThreads directive specifies the maximum number of idle threads; leave the default as is. In the default-threaded mode, Apache kills child processes to control minimum and maximum thread count.

## ThreadsPerChild

This directive defines how many threads (25 by default) are created per child process.

![](img/9eb7e89292d2f85707b4d49102c865b7_322_0.png)

Because on Windows there is only one child process and it owns all the threads, if you are running Apache on a Windows system you should set ThreadsPerChild to the maximum number of simultaneous requests you want to handle.

## MaxRequestsPerChild

This directive sets the number of requests a child process can serve before getting killed. The default value of 0 makes the child process serve requests forever. I do not like the default value because it allows Apache processes to slowly consume large amounts of memory when a faulty mod_perl script or even a faulty third-party Apache module leaks memory. If you do not plan to run any third-party Apache modules or mod_perl scripts, you can keep the default setting or else set it to a reasonable number. A setting of 30 ensures that the child process is killed after processing 30 requests. Of course, new child processes are created as needed.

## Configuring the main server

The main server configuration applies to the default Web site that Apache serves. This is the site that will come up when you run Apache and use the server's IP address or host name on a Web browser.

### Port

The very first directive in this section of the httpd.conf file is the Port directive, which sets the TCP port that Apache listens to for connections. The default value of 80 is the standard HTTP port. If you change this to another number such as 8080, you can only access the server using a URL such as http://hostname:8080/. You must specify the port number in the URL if the server runs on a non-standard port.

![](img/9eb7e89292d2f85707b4d49102c865b7_323_0.png)

> There are many reasons for running Apache on non-standard ports, but the only good one I can think of is that you do not have permission to run Apache on the standard HTTP port. As a non-root user you can only run Apache on ports higher than 1024.

After you have decided to run Apache on a port, you need to set the User and Group directives to tell Apache the user and group names to use. These two directives are very important for security reasons. When the primary Web server process launches a child server process to fulfill a request, it changes the child's UID and GID according to the values set for these directives. If the child processes are run as root user processes, this can lay your server open for attack by hackers. I highly recommend that you run the child server processes as a very low privileged user belonging to a very low privileged group. In Red Hat Linux, the user named nobody (usually UID = -1) and the group named nogroup (usually GID = -1) are low privileged, and are ready made for this purpose. You should consult your /etc/group and /etc/passwd files to verify these settings.

By taking the precaution of running the primary Web server as a non-root (regular) user, the server will not be able to change the UID and GID of child processes because only root user processes can change the UID or GID of other processes. Therefore, if you run your primary server as the user named ironsheik in a group named sheiks, all child processes will have the same privileges of ironsheik and the sheiks group.

![](img/9eb7e89292d2f85707b4d49102c865b7_324_0.png)

If you plan on using the numeric format for the user and/or group IDs, you need to insert a # symbol before the numeric value. You can find numeric IDs in the /etc/passwd and in /etc/group files.

### ServerAdmin

ServerAdmin defines the e-mail address that is shown when the server generates an error page. Set this to your e-mail address or that of the administrator you want to specify.

### ServerName

Now you need to set the host name for the Server using the ServerName directive. This directive is commented out by default since Apache install cannot guess what host name to use for your system. So, if your host name is called www.domain.com, set the ServerName directive accordingly. Be sure, however, that the host name you enter here has proper domain name server (DNS) records that point it to your server machine.

### DocumentRoot

Like all other Web servers, Apache needs to know the path of the top-level directory where Web pages will be kept. This directory is typically called the document root directory. The DocumentRoot directive instructs the server to treat the supplied directory as the root directory for all documents.

![](img/9eb7e89292d2f85707b4d49102c865b7_324_1.png)

Be careful what directory you specify; this is a very important decision. For example, if the directive is set to the / (root) directory, every file on the system becomes accessible by the Web server. Of course, you can protect files by providing proper file permission settings, but setting the document root to the physical root directory of your system is definitely a major security risk.

The best place to point the DocumentRoot directive to is a specific sub-directory of your file system. If you have used the --prefix=/usr/local/apache option in configuring the Apache source, this directive will be set as follows:

```
DocumentRoot "/usr/local/apache/htdocs"
```

![](img/9eb7e89292d2f85707b4d49102c865b7_325_0.png)

Just because your document root points to a particular directory, this does not mean the Web server cannot access directories outside your document tree. You can easily enable it to do so using symbolic links (with proper file permission) or using aliases. From an organizational and security-conscious perspective, I don’t recommend using a lot of symbolic links or aliases to access files and directories outside your document tree. Still, it’s sometimes necessary to keep a certain type of information outside the document tree, even if you need to keep the contents of such a directory accessible to the server on a regular basis – just be careful that you don’t inadvertently open a back door to your system. If you have to add symbolic links to other directory locations outside the document tree, make sure that when you back up your files, your backup program can back up symbolic links properly.

### Option and AllowOverride

The Option and AllowOverride directives are enclosed in a <Directory> container as follows:

```
<Directory />
    Options FollowSymLinks
    AllowOverride None
</Directory>
```

The scope of the enclosed directives is limited to the named directory (with any subdirectories.); however, you may only use directives that are allowed in a directory context.

In this directive, the Options and the AllowOverride directives apply to DocumentRoot, which is the top-level directory of the main Web site. Because directives enclosed within a directory container apply to all the subdirectories of the named directory, the directives apply to all directories within DocumentRoot and all of its subdirectories.

The Options directive is set to FollowSymLinks, which tells Apache to allow itself to traverse any symbolic link within DocumentRoot. Because the Options directive is only set to follow symbolic links, no other options are available to any of the directories within DocumentRoot. So implicitly, the Options directive is as follows:

```
Options FollowSymLinks -ExecCGI -Includes -Indexes -MultiViews
```

However, be assured that the main idea behind such a restrictive default value for the Options directive is to create a very closed (i.e., secure) server. Because only symbolic link traversal is allowed, you must explicitly enable other options as needed on a per directory basis. This is a very good thing from a security prospective. The next directory container opens up the DocumentRoot directory as shown below:

```
<Directory "/usr/local/apache/htdocs">
    Options Indexes FollowSymLinks MultiViews
    AllowOverride None
    Order allow,deny
    Allow from all
</Directory>
```

If your DocumentRoot is different, change the named directory path. Here is what the above configuration means to Apache:

- The named directory and its subdirectories can be indexed. If there is an index file, it will be displayed; in the absence of one, the server creates a dynamic index for the directory. The Options directive specifies this.
- The named directory and all its subdirectories can have symbolic links that the server can follow (that is, use as a path) to access information. The Options directive also specifies this.
- The named directory and all its subdirectories can be part of content negotiations. The MultiViews option for the Options directive sets this. For example, when the given Options directive is enabled within the DocumentRoot directory as shown above, a request for www.domain.com/ratecard.html can be answered by a file called
