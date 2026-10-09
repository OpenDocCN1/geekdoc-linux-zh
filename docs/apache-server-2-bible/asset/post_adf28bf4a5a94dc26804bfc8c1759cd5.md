
Figure 17-4: Example servlet listings.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_519_0.png)

Figure 17-5: Output of `/examples/servlet/HelloWorldExample`.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_519_1.png)

As you can see, this is a fairly simple servlet—it simply prints out a bunch of HTML tags to create the output.

### Running your own servlets or JSP

This section teaches you to configure your own servlets to run via `mod_jk`. Say that your servlet is called `myapp`. Here is what you need to do to get it working with Apache and Tomcat:

1. Create the following configuration in `/var/tomcat/conf/server.xml`:

```xml
<Context path="/myapp"
    docBase="/var/tomcat/webapps/myapps"
    debug="0"
    reloadable="true" >
  </Context>
```

The path attribute specifies the path in the URL that will refer to your servlet called myapp. The docBase attribute specifies the path where this servlet is found. This can be either an absolute path or a path relative to the Tomcat Context Manager (which by default is $TOMCAT_HOME/webapps). The debug attribute specifies the level of debug logging messages, and the reloadable attribute specifies whether Tomcat will reload a servlet automatically when it is changed.

2. Stop and restart Tomcat using `/usr/bin/tomcat stop ; /usr/bin/tomcat start` command. This will generate a new `/var/tomcat/conf/mod_jk.conf.auto` file, which should have this configuration segment:

```apache
Alias /myapp "/var/tomcat/webapps/myapp"

<Directory "/var/tomcat/webapps/myapp">
    Options Indexes FollowSymLinks
</Directory>

JkMount /myapp/servlet/* ajp12
JkMount /myapp/*.jsp ajp12

<Location "/myapp/WEB-INF/">
    AllowOverride None
    deny from all
</Location>

<Location "/myapp/META-INF/">
    AllowOverride None
    deny from all
</Location>
```

3. Create the `/var/tomcat/webapps/myapp`, `/var/tomcat/webapps/myapp/WEB-INF`, `/var/tomcat/webapps/myapp/WEB-INF/classes`, and `/var/tomcat/webapps/myapp/META-INF` directories.

4. Store the web.xml configuration file for the myapp servlet in `/var/tomcat/webapps/myapps/WEB-INF` directory.

5. Copy the servlet classes for myapps to the `/var/tomcat/webapps/myapps/WEB-INF/classes` directory.

6. Make sure the Tomcat user (that is, the user ID used to run Tomcat) can access the new `/var/tomcat/webapps/myapps` (including all subdirectories and files) directory.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_521_0.png)

**Figure 17-6:** Simplified source code of /examples/servlet/HelloWorldExample.

That’s it! You should be able to access the servlet using http://your_web_server/myapps.

♦ ♦ ♦

# Securing Your Web Site

Ensuring Web site security is a critical part of a Web administrator's job. In this part, I discuss the various security issues that can arise with Apache, and how to resolve these issues by using various tools, techniques, and policies or guidelines. I also show you how to turn your Apache server into a Secure Socket Layer (SSL)-capable Web server using either the mod_ssl or Apache-SSL modules.

# PART IV

# In This Part

- Chapter 18 Web Security
- Chapter 19 Securing Apache with SSL

# 18

# C H A P T E R

# Web Security

**T**he need for security is often unclear to novice administrators. Many administrators think about security only after a breach of security has occurred—too late! This chapter provides an idea of the hidden risks that make security so important.

# Understanding Web Security

The moment you get your Web server up and running and available to the rest of the world, you open a window for others to get into your network. You intended to do this, right? Most people will use the information available on your Web site, but some may look for holes in this window so that they can get to information that they are not supposed to access. Some of these people are vandals who want to create embarrassing situations, and some are information thieves. Either way, if anyone succeeds in finding that hole, you may find your Web sites mutilated with obscene materials, or you might even lose confidential data. Sometimes the attacks do not affect your site directly. The infiltrators may use your server and other resources to get to another network, putting you at legal risk. None of these scenarios is desirable.

To avoid such risk and embarrassment, this chapter shows you how to secure your Web sites. I assume that the following security requirements are applicable for your Web site:

- Maintaining the integrity of the information you publish on the Web.
- Preventing the use of your Web server host as a point for break-ins into your organization's network (which could result in breaches of confidentiality, integrity, or availability of information resources).
- Preventing the use of your Web server host as a staging area for intrusions into other networks (which could result in your organization being liable for damages).

# In This Chapter

Understanding Web security

Knowing the security checkpoints

Choosing an administrative security policy

Recognizing and minimizing CGI and SSI security risks

Protecting your Web content

Most Web security incidents occur because confidential information is made vulnerable by improperly configured software. The software could be the Web server itself, or applications (such as CGI programs, Server-Side Includes, and Server API applications) that are run by the Web server. This can result in the inadvertent disclosure of confidential information. Subsequent attacks can be launched by exploiting the confidential information.

If your Web server configuration is tight and the applications run by the Web server are fairly secured, are you done? No, because the attacks could be targeted to the Web server via different routes. Your Web server might become compromised by way of totally unrelated applications, or by a bug in the operating system, or by poor network architecture.

To be secure, you have to look at each and every detail. This can be a daunting task; but remember that it is impossible to have a completely secured environment. There is never a foolproof solution to all security issues, because all issues are not known. Your goal is to improve your security as much as possible.

## The Security Checkpoints

The very first step in protecting your Web server from vandals is to understand and identify the risks involved. Not too long ago, Web sites only served static HTML pages, which made them less prone to security risks. The only way a vandal could hack into such Web sites was to break into the server by gaining illegal access. This was typically done by using a weak password or by fooling another daemon (server) software. However, most Web sites no longer serve static HTML pages; they serve dynamic contents that are often personalized to provide a rich user experience. Many Web sites tie in applications to provide valuable customer service or to perform e-commerce activities. This is when the risks start to weigh more and more. Yes, Web applications are the heart of the Web security problem. Most Web sites that have been hacked by vandals were not vandalized because of the Web server software. They were hacked because of one or more holes in the application or script that the Web server software ran.

There are several security checkpoints that you need to review to improve the security of your public Web sites; Figure 18-1 shows the overall security checkpoint diagram. This diagram identifies the security checkpoints that must be examined thoroughly before considering an Internet-connected network secure.

There are three primary checkpoints:

- Your network: This is the outer most checkpoint, which needs to be very strong. Your network connects to the Internet via either a router, firewall system, or a gateway server. Therefore your network is a primary security checkpoint. Securing your network should be your primary security concern.
