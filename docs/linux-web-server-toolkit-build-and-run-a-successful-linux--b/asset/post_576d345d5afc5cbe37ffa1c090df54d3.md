
## Chapter 10: Basic Scripting and Forms

application. This can include tables, graphic tags (<IMG>), tables, and any other HTML tags.

When you've written out all the necessary HTML, just make sure the script exits. The Web server will have captured all the text and returned it to the browser.

## Summary

In this chapter, you've learned how to use server-side includes and create forms and cgi-bin scripts on your Web server to interact with form data. You've seen how to personalize your Web site by including forms and enabling it to respond to inquiries, and you've seen some basic script samples for processing data. In this chapter you've learned the following:

- * Server-side includes (SSI) are a simple method for customizing HTML pages but they are limited in their capabilities and pose some special security threats.
- * Web page forms are easy to create using a few HTML tags. Each tag defines a part of the interface where a user can select or enter data.
- * Data from forms is returned by the Web browser to the Web server, where scripts that you write can process the data to create a customized response to the users' data.

By studying sample forms and scripts, you can imitate commonly used tasks to create your own forms and Web server scripts quickly. In the next chapter, you'll begin configuring your Apache Web server, completing the initial set up that you reviewed in Chapter 7. You'll learn about security settings and about how to create automatic directory listings and set all the server information to optimize the performance of your Web site.

## Chapter 11

## Configuring the Apache Web Server

IN THIS CHAPTER, YOU'LL learn all about the configuration files that control the Apache Web server. The different options in each file are explained, along with some methods to tune and optimize your server according to how your Web server is configured to serve the needs of your organization. Topics in this chapter include:

- Understanding how your server operates
- Setting up server configuration
- Setting up server resources
- Setting up security options
- Adding advanced features

## Understanding How the Server Operates

A Web server operates in the same way as any other networking program on your Linux system. After you start it, it reads its configuration files and then begins monitoring a specific network port – 80 is the default for the Web – to check for requests it can process. The Web server is started automatically in the OpenLinux Lite system. The port uses and the initialization to start monitoring that port are all controlled in the standard Linux fashion, according to information stored in the /etc/inetd.conf and /etc/services files.

Early Web servers (httpd) were designed to start another copies of the Web server program for each incoming request. Each copy served the request it had received and shut down, while a master process kept receiving new requests and starting new processes to handle them.

That system worked well, but with larger Web servers, it became a lot more efficient to use a master process that kept several other Web server processes going all the time, instead of starting and stopping them for each incoming request. If the load of Web requests over time was higher, the number of extra Web processes was increased. This system is used by the Apache Web server, and provides a higher level of overall performance than the previous method.

The result is that if you use the ps -aux command to list the processes running on your system, you'll see many copies of the httpd program running. This is normal. You'll learn in this chapter how to control the number of Web server processes according to your system load.

## Starting and Stopping the Server

The Apache Web server is started during the boot process and is always running in the background. When you add or change information in the Apache configuration files, you have to tell the Web server to reread the configuration files so the new information takes effect.
UNIX provides a command that effectively reinitializes a program. This is done by sending a particular signal to the Web server.
After you've made changes to your configuration files, you can either shut down and restart your web server or enter the following command to update the configuration without interrupting Web service:

```
kill -s SIGHUP 'cat /var/run/httpd.pid'
```

This command sends a "restart" signal to the master httpd process, telling it to stop and restart, rereading all the configuration files.

## Understanding Basic Web Security

Although you read some things about Web security in Chapter 10 on writing scripts, configuring the Web server involves some additional security issues. Overall, you'll be concerned about the following three types of potential security problems:

- Accessing access to Web documents – those reserved for certain groups or individuals
- Accessing access to other parts of your system, so that unauthorized users can't access system configuration files, execute programs, and so forth outside the scope of the Web server itself
- Preventing actions by users that make your Web server unable to respond to other users' requests – this is called a Denial of Service attack

The configuration files you'll set up in this chapter will take care of both types of security.

## Chapter 11: Configuring the Apache Web Server

## Using Multilevel Configurations

The configuration files described in this chapter apply to every copy of the Apache server started on your system. Apache provides a way, for different configuration settings depending on the location of the file requested by a user. For example, you might want the overall configuration to block directory listing, but in one area, you want to select from a directory listing because the contents change each day and you don't want to update an HTML page.

Each directory can contain a configuration file that applies to everything in that directory and everything below it. The default name of file is .htaccess (it starts with a period it is a hidden file). You can set its name to anything you choose. You can also set an option so that no local, directory-specific configuration files are be used. This provides additional security and improves performance because the configuration files don't have to be read and implemented for every request processed by the Web server.

The performance hit can be heavy if you use a lot of per-directory configuration files because of the inheritance feature. For example, if a user requests the file /doc/products/reviews/june.html the Web server must check each subdirectory in that path to see whether changes or additions are made to the configuration settings. Anything in the .htaccess file within the directory documents/ must be processed; then changes and additions in the products/ subdirectories are reviewed, then those in reviews/. This must be done for each Web request.

Although it's a useful feature if you really need it, if you don't need per-directory configuration, you'll improve performance and decrease security concerns. The main reason for using per-directory configuration is when different people control sections of your Web site, such as users' home pages, marketing information, and technical support documents.

## Configuration File Layout

Each of the configuration files for the Apache server is a plaintext file that lists options and settings for the server. The syntax is very simple, with the following two types of options:

- A Directive (command) followed by the options that apply for that directive
- An HTML-style container, such as <Directory directory-name>, where all the directives between the opening and closing tag apply to the directory given in the tag

The directives described in the sections that can appear in any of the three configuration files: httpd.conf, srm.conf, and access.conf. The three files exist mostly for historical reasons. For clarity, however, it's a good idea to keep server-level
