
## Chapter 23: Software Development on Ubuntu

As you might expect, your mileage may vary when importing existing source projects into Eclipse, but the ease with which you can do makes it easy for you to move your existing application development efforts into Eclipse so that you can take advantage of its many capabilities and the ease-of-use that a modern IDE like Eclipse provides.

## Getting More Information about Eclipse

Eclipse is a powerful, full-featured IDE, which means that the examples in the previous two sections can only scrape the surface of its capabilities and bells and whistles. For more detailed information about using Eclipse, see one of the many books on using Eclipse that are available, or visit some of the following resources on the Web.

- www.eclipse.org: home page of the Eclipse mothership
- www.eclipse.org/documentation: Eclipse documentation site
- http://planeteclipse.org/planet: Planet Eclipse, frequented by Eclipse developers, contributors, and users
- www.eclipseplugincentral.com: Eclipse Plug-in Central, from which you can download many free Eclipse plug-ins

The next section talks about source code control software, highlighting Subversion. As an example of the wide range of free plug-ins for Eclipse, the following are two free Subversion plug-ins for:

- Subversive Plug-in at www.polarion.org
- Subclipse Plug-in at http://subclipse.tigris.org

Not only do these plug-ins provide an easy way to work with Subversion repositories in Eclipse, but they also provide a great example of how all of this open source tends to fit nicely.

## Source Code Control Software

If you've ever accidentally deleted a source file that you were working on, lost the version of your Great American novel when your system crashed and scrambled its disks, or worked on a joint project with someone who was thoughtful enough to overwrite all of your new code, you might have wished you'd been using a source code control system until you finished shearing. A source code control system, popularly known as an SCCS, is a software package that manages a repository of source code, tracking changes to existing code, managing different versions of that code (often known as branches), and providing a mechanism for recovering any version of file in the repository at any point in time.

If I had to count the number of times that an SCCS has saved my back when doing development, I would quickly run out of fingers and toes. This doesn't necessarily mean that I'm sloppy.

When multiple developers work on the same sets of files, conflicts between their changes are bound to occur. As SCCS provides a mechanism for identifying and resolving conflicts of changes (known as merges). Similarly, a source code control system facilitates experimentation with code by providing a safety net that you can use to fall back to versions of files you know to be working, just in case your latest bright idea didn't turn out to be very illuminating after all.

## Caution

Common misconception is that an SCCS is a replacement for backups. Not really true. SCCS may be a replacement for backing up your own files, because you can check in and retrieve them later if your machine bursts into flames. the SCCS repository itself must be backed up regularly — anything, a central repository used across a project or enterprise provides a single, critical point of failure.

The next two sections discuss the most common source code control systems for Linux.

If you're just reading this section because you're looking for a recommendation for a source code control system, skip to the section on Subversion. Source control systems such as Git and Mercurial are gaining in popularity and offer many advantages, but Subversion is kid-tested and mother-approved without the messy scent of ancient history that accompanies CVS.

## The Concurrent Versioning System (CVS)

My humorous comments about CVS in the previous section are meant to be that, and should not be taken to mean that CVS is not a time-tested, stable SCCS. CVS is still in use for development for years and is over the Internet. That said, most projects that I'm aware of which have traditionally depended on CVS are moving elsewhere, and that's a trend that I believe will continue, if not accelerate. However, if you're a CVS fanatic or your current projects already depend on CVS, you can use your favorite Package Management tool to install CVS, and then see sites as the following for information about setting up Web-enabling CVS repositories:

- http://faqs.org/docs/ldev/0130091154_198.htm: The Linux FAQ's section on CVS
- http://flexwiki.com/default.aspx/FlexWiki/ConfiguringCVS.html: A nice wiki that provides a lot of good information about understanding and using CVS

CVS is a fine system, and I've used it extensively at many companies. However, I feel that you're going to set up an SCCS from scratch on your Ubuntu system, you may well use using from this century.

## Chapter 23: Software Development on Ubuntu

## Installing and Using Subversion

Subversion (http://subversion.apache.org) is an extremely popular source code control system. Aside from its power and command set, much of Subversion's popularity lies in the fact that it is based on WebDAV (Web Distributed Authororing and Versioning), a Web-based protocol that enables you to view and access Subversion repositories in any Web browser. This includes the ability to drag-and-drop files from your Web browser to your desktop to check them out, and vice versa to check them in. As you'll see in the next sections, setting up a Subversion repository and integrating it into your Web server is easy to do, just as Subversion is easy to use from the desktop or the command line.

### Tip

Another common way of setting up Subversion is to access its repositories through SSH (Secure Shell). For a great explanation of setting up svn in this way, see www.startupto.com/server-tech/subversion/setting-up-svn. Though it discusses Subversion in this fashion on CentOS rather than Ubuntu, the instructions are distribution-independent after the initial installation.

### Installing Subversion

You can install Subversion using any of the commands in Chapter 19. When installing Subversion, I generally install the following packages, not all of which are required. My rationale for each name of the package in this list:

- apache2 (Optional): This package is necessary only if you want to provide a Subversion repository that users can access through your Web server. Selecting this item causes the Apache2 Web and related files to be installed on your system. I always find it handy to be able to access my repository over the Web, it's easy to configure everything at once, and the extra disk space that Apache2 consumes is always worth it to me. However, you can always add this later. See Chapter 29, "Setting Up a Web Server," for information about manually installing different versions of.
- subversion (Mandatory): This is the core Subversion package.
- apache2-svn (Optional): This provides the Apache module module for Subversion.

## Part II: Ubuntu for Desktop Users

### Tip

Another common way of setting up Subversion is to access its repositories through SSH (Secure Shell). For a great explanation of setting up svn in this way, see www.startupto.com/server-tech/subversion/setting-up-svn. Though it discusses Subversion in this fashion on CentOS rather than Ubuntu, the instructions are distribution-independent after the initial installation.

### Installing Subversion

You can install Subversion using any of the commands in Chapter 19. When installing Subversion, I generally install the following packages, not all of which are required. My rationale for each name of the package in this list:

- apache2 (Optional): This package is necessary only if you want to provide a Subversion repository that users can access through your Web server. Selecting this item causes the Apache2 Web and related files to be installed on your system. I always find it handy to be able to access my repository over the Web, it's easy to configure everything at once, and the extra disk space that Apache2 consumes is always worth it to me. However, you can always add this later. See Chapter 29, "Setting Up a Web Server," for information about manually installing different versions of.
- subversion (Mandatory): This is the core Subversion package.
- apache2-svn (Optional): This provides the Apache module module for Subversion.

## Setting Up a Subversion Repository

Creating a Subversion repository is done with the svnadmin command, which creates the directory structure that makes up a Subversion repository. This command takes one argument, which is the name of the directory in which you want your Subversion repository to be created.

One important thing to remember when creating a Subversion repository is that, because Subversion depends on WebDAV, which depends on the HTTP protocol, your Subversion repository must be owned by the user and group that is used for communication via this protocol. On Ubuntu, this is the www-data user and the www-data group.

### Tip

If you are creating a Subversion repository named svn and plan to export it through a Web server by that name, you must not create it in your Web server's DocRoot directory. You will see later in this section, you specify the full pathname to the Subversion repository in Apache's Sub configuration file. Trying to use a repository named svn that is located in your Web server's DocRoot directory will result in the error 301 Moved Permanently (http://server-name), which isn't intuitive.

For example, to create a Subversion repository in the directory /var/svn, you would execute the following command:

```
$ sudo -u www-data svnadmin create /var/svn
```

After supplying your password, the svnadmin command creates your repository and populates it with the subdirectories it requires, all owned by the proper user and group. You can verify this by listing the contents of the specified directory, as in the following example:

```
$ ls -1 /var/svn
total 28
drwxr-xr-x 2 www-data www-data 4096 2010-01-29 12:31 conf
```
