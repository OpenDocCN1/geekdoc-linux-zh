
## Content Management Systems

A Content Management System (CMS) assists a software or Web developer in organizing and facilitating any collaborative process and its final outcome. The term “content management” loosely refers to not only the checking in and out of files, but also the generalized sharing of information, such as common calendars, wikis, and the like. The earliest Content Management Systems emerged around 1975 when mainframes and electronic publishing required really began to catch on. These earliest versions were basically nothing more than general repositories that enabled multiple users to participate in the same project.

As computer systems became more and more complex, the need to effectively manage content also becomes more complex. As the Internet came to fruition, so did the wave of CMSs. Now there are more CMSs than you can shake a stick at. The goal of this chapter is to try and wade through all the muck to help you define whether you need a CMS, which variety of CMS is right for your project, and how you can use a CMS to improve your efficiency.

## Types of CMSs

CMSs come in all shapes and sizes, and can basically manage anything being worked on by a team of individuals. From managing simple static website content, to allowing collaborative documentation across the Internet (wiki), CMSs perform many functions. CMS packages can generally be classified into two categories: Enterprise CMSs and Web CMSs.

## Enterprise CMSs

These high-powered software packages are usually comprehensive solutions, delivering effective content management for use on an enterprise, or corporate level. They are designed to help a corporation become more efficient and cost-effective, and increase accuracy and functionality, while decreasing human error and customer response times.

They can integrate corporate functions such as shipping and delivery systems, invoicing, employee and human resource issues, customer relations, and document management and transactional (sales) systems. Enterprise CMSs bring data management down to the user level so many users can add their individual piece to a very large integrated pie. Software companies deploying these complex systems pride themselves on offering highly customized company-wide solutions, and the software usually comes with a relatively hefty price tag.

## Web CMS/Portals

Web CMS packages are mostly created for use on the web. They can incorporate numerous functions, or have one specific function they are centered around. They allow users to update portions of a common Web site or collaborate in a website "community." Web CMSs can make a developer’s life easy by bringing functionality to a website quickly and easily, and allowing a lead developer to include others in site development and maintenance without fear of straying from the standards. Open source Web CMS packages will be the focus of this chapter, in particular the PHP/MySQL packages.

A subset of the Web CMS category is groupware. This type of package runs over an intranet or over the Internet and is designed to allow collaboration between users, presumably working for the same company, working on the same projects. They typically offer features such as project management, file checking in and out, calendar systems, email, and internal forums.

## Open Source Web CMS Packages

Common functions of a Web CMS include:

-   **Static web page updates:** Updates content without altering look and feel of site.
-   **Weblogs (blogs):** Online journals.
-   **Wiki:** Collaborative documentation projects.
-   **Publications:** Posting and organization of news articles.
-   **Managed learning environments:** Web-based learning.
-   **Transactional CMS:** E-commerce functions.
-   **Image and file galleries:** Compilation of images or files for public use.
-   **Forums:** Bulletin board systems fostering discussions between users.
-   **Chat rooms:** Real-time chatting between users.
-   **RSS feeds:** Allows users to download content.
-   **Polls:** Allows users to vote on a topic.
-   **Calendar systems:** Web-based multi-user calendars.

There are numerous other functions that could be considered underneath the CMS realm, but these are the major ones and the ones on which this chapter focuses.

First, take a look at some of the more comprehensive open source CMS packages.

### All-Inclusive Web CMSs

Like fancy tropical resorts that wrap up your vacation all into one nice neat package, these comprehensive Web CMSs can do as little or as much as you like. The following sections introduce you to some of the more popular packages available, although a myriad of these can be found on websites such as [http://www.sourceforge.net](http://www.sourceforge.net). This text does not go into detail about installation on these packages, as you’ve probably had some experience in this department in the past. However, if there are any special considerations regarding installation, they will be duly noted. As well, you need to have all aspects of the LAMP system working properly before installing these packages.

Most all-inclusive Web CMSs have common functionality such as changing user permissions, modifying site layout, changing server settings, and so on. One thing that should be mentioned is that there is a lack of transactional CMS interfaces (shopping carts for *e*-commerce) with many of the so-called comprehensive CMS packages available.

#### ExponentCMS

ExponentCMS is available at [http://www.exponentcms.org](http://www.exponentcms.org) . At the time of this writing, the most current version is 0.96.3, and is what this section is based on. On the Exponent/Sourceforge interface at [http://sourceforge.net/projects/exponent/](http://sourceforge.net/projects/exponent/) , you can find links to screenshots, documentation, contributions, and the standard Sourceforge information.

##### Installation Notes

Installation is relatively simple, and the only thing you need to know before installation is that you will need to create a database. This applies to both remote and local installations. You will also need to have a user and password set up, as you will be asked to supply all that information during the installation process.

##### General Overview/Default Installation

Installing this CMS gives you several features that are “active” by default. These are:

-   **Address Book:** Organizes contact information.
-   **Admin Control Panel:** Easy-to-use interface for administering the site.
-   **Calendar System:** Keeps track of events with different views.
-   **Contact Form:** Allows visitors to the site to contact you.
-   **Image Manager:** Works with other modules to manage images on the site.
-   **Preview Link:** Lets those working on the site preview their work.
-   **Private Messaging Center:** Allows users to send emails or private messages to one another.
-   **Resource Manager:** Organizes and displays uploaded files.
-   **Text Module:** Displays text and keeps track of revisions.
-   **Weblog/Online Journal Manager:** Organizes blog entries.

The “inactive” features (those you can simply turn on) are:

-   **Banner Manager**: Manages banner ad campaigns and click-throughs.
-   **Content Rotator**: Displays different images or text to the user each time they visit the site.
-   **Flash Animation Manager**: Organizes a Flash Animation.
-   **Form Module**: Manages any forms on the site.
-   **HTML Template Manager**: Manages uploaded HTML templates.
-   **Login Module**: Allows users to log in to the site.
-   **Multi-site Manager**: Allows you to create and manage other sites.
-   **Navigator**: Manages the navigation system.
-   **News Feed System**: Organizes and displays news articles.
-   **Search**: Allows users to search the site.
-   **UI Switcher**: Gives users with the correct permissions the ability to switch from user to administrator.

Through the easy-to-use admin Module Manager, you can activate or deactivate any of these modules with the click of a button.

Other modules are available for downloading from [http://www.sourceforge.net](http://www.sourceforge.net), With the Extension Upload Manager, installing modules is easy; you don’t even need to unzip them. These extensions include:

-   **Article Manager**: Organizes and displays articles on the site.
-   **Bulletin Board**: Manages site forum.
-   **FAQ**: Manages the FAQ section of the site.
-   **Image Gallery**: Allows users to rank and view images.
-   **Listing Manager**: Organizes and manages listings, such as real estate listings.
-   **Page Dispatcher**: Allows you to upload and display dynamically generated pages (such as PHP).
-   **Slideshow**: Manages slideshows on the site.

Besides installing, activating, and deactivating site modules, as the site admin you can import data (such as a user list in csv format) through the admin interface. This makes it easy for you to convert from another system or from an internal database.

There is the WYSIWYG HTMLArea editor also embedded into the software, making it easy for your authors and contributors to add text. As an admin, you also have control over the HTMLArea toolbar, which lets you determine what text options your users have.

## Customizing the Default Settings

Like most other CMS packages, you can alter user settings in the Admin Control Panel. With Exponent CMS, you can set approval policies based on users and content, although this CMS is module-focused as opposed to user-focused. For example, you could create an approval policy for the Calendar module
