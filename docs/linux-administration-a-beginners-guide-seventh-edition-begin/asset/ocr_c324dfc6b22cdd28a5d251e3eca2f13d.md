# 494 Linux Administration: A Beginner's Guide

# Quick How-To: Serving HTTP Content from User Directories

After enabling the UserDir option, and assuming the user yangang want to make some web content available from within her home directory via the web server, these steps will make this happen:

+   1. While logged into the system as the user yangang, create the public_html folder:
2. Set the proper permissions for the parent folder:
3. Set the proper permissions for the public_html folder:
4. Create a sample page index.html under the public_html folder:

```
yangang@server:~$ mkdir ~/public_html
```

```
yangang@server:~$ chmod a+x
```

```
yangang@server:~$ chmod a+x public_html
```

```
yangang@server:~$ echo "Ying Yang's Home Page" >> \
~/public_html/index.html
```

As a result of these commands, files placed in the public_html directory for a particular user and set to world-readable will be on the web server. To access the contents of that folder via HTTP, you would need to point a web browser to this URL:

```
http://YOUR_HOST_NAME>/-<USERNAME>
```

WHERE YOUR_HOST_NAME is the server's FQDN or IP address. And if you are sitting directly on the web server itself, you can simply replace that variable with localhost.

For the example shown here for the user yangang, the exact URL will be http://localhost/-yangang. And the IPv6 equivalent is http://[::]/-yangang.
Note on older versions of Red Hat-like distros with SELinux subsystem enabled, you may have to do a little more to get the UserDir directive working. This is because of the default security contexts of the files stored under each user's home directory. By default, the context is user_home_t For this functionality to work properly, you will have to change the context of all files under ~/username/public_html to http_sys_content_t. This allows Apache to read the files from the public_html directory.

```
[yangang@fedora-server ~$] chcon -Rt http_sys_content_t public_html/
```