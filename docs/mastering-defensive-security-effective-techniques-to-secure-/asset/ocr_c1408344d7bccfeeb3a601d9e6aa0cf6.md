As a fun fact, notice that the -g option allows you to process Google dork results as target URLs.

# Weevely

Weevely is a very interesting tool that provides a web shell to attack web applications. It has a lot of interesting features, including the following:

+   - HTTP and HTTPS proxies to browse through the infected web application.
- Ability to brute force SQL accounts on the targeted system.
- Mount the remote filesystem.
- Direct shell access to the target.
- Upload and download files.
- File navigation and more.

I am sure that you would love to see an attack with this tool, so let's do a quick lab to show you how Weevely works.

For this lab, we will use DVWA as the target machine on our Kali Linux machine.

> Tip
In Chapter 12, Mastering Web App Security, we covered the installation and setup of DVWA, so if you have not installed it, then just go back to that chapter and follow our simple steps to get it up and running.

Now, assuming that you have DVWA already installed on your Kali Linux machine, we just need to go ahead and run it.

The first step will be to start the database services with the following command:

```
sudo service mysql start
```

Then, let's start the Apache server with the following command:

```
sudo service apache2 start
```