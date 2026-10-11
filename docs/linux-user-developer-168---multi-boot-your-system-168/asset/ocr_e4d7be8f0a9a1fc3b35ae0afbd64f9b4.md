# Organise collaborative projects with Ganib

Discover how to install Ganib and use it to manage and simplify your collaborative projects

![](bbox=[0.06, 0.32, 0.19, 0.41])

**Nithish Tiwari** is a software developer by profession, with a huge interest in free and open source software. As well as serving as community moderator and author for leading FOSS publications, he also helps organisations adopt open source software for their business needs.

# Resources

+   * Ganib
+   http://www.ganib.com/

![](bbox=[0.2, 0.32, 0.91, 0.59])

**Software development is one of the fastest growing fields in IT, but it has its own problems.** There are remotely distributed teams, working on the same code repository. There are changing priorities and deadlines. There are changing requirements and new technologies coming up. In addition, with its intangible outputs, software development proves very difficult to measure. So how do you manage all this while making progress?

![](bbox=[0.57, 0.61, 0.91, 0.69])

Agile development methodology has given us some hope. Agile focuses on the end product, while ignoring trivial things like lines of code written or man-hours spent, thus eliminating the need to measure effort and rather measure the completion of the final product. But then there is a dearth of good open-source, agile-focused tools; most of the tools are old, tweaked to support agile. With Ganib, this is set to change. Ganib is an open source project management tool with support for agile scrum, real-time tracking, bug tracking and various other features. It also supports integrations with third party tools like Microsoft Project, LDAP and so on to facilitate seamless working. In this tutorial, we'll take a closer look at Ganib and its features. But before that, let's start with the installation process. We've used Ubuntu 14.04 as the platform of choice for installation.

# **01** Installation preconditions

Ganib can be installed on any of the major OS platforms. As mentioned earlier, we have taken Ubuntu 14.04 as the base platform for this tutorial. To get started, you should have JRE and MySQL installed on your system. Apache Tomcat is required as well, but it is bundled along with the Ganib installer. So, let's first see how to install MySQL. The installation is simple; update your package index, install the mysql-server package, and then run the included security and database initialisation scripts. Just open a command prompt and type the following commands.

```
$ sudo apt-get update
$ sudo apt-get install mysql-server
$ sudo mysql_secure_installation
$ sudo mysql_install_db
```

> **Above right**
> The Ganib homepage depicting various features. In the middle, you have the burn down chart, followed by the billing hours