# Chapter 13

+   1. Very detailed user permissions are allowed, making it simple and straigthforward to see who is allowed to do what.
+   2. Default modules are extensive, making a comprehensive site less labor-intensive for the developer.

The only weakness is that currently, the system does not allow breaking of the traditional two- or three-column layout.

phpWebsite is a nice “middle-of-the-road” CMS, balancing a high level of built-in functionality with a high degree of user interactivity. If you are looking for a package that can support a medium-sized group of contributors, and still foster visitor interactivity, then this might be the CMS for you.

# TikiWiki

This software is available at [http://www.tikiwiki.org](http://www.tikiwiki.org), and the current version available at the time of this writing is 1.9.0.

# Installation Notes

If you are using older versions of PHP (older than 4.3) or MySQL (older than 4.0.1), then you will want to pay particular attention to the “Requirements and Setup” documentation, which can be found [http://doc.tikiwiki.org/tiki-index.php?page=requirements+and+setup](http://doc.tikiwiki.org/tiki-index.php?page=requirements+and+setup). Other points to note are:

+   1. The PDF Generation module needs the php-xml package to be installed.
+   2. Because of the use of sessions, make sure your php.ini file has the following settings:
+      1. session.save_handler = files
+      2. session.save_path = /tmp (for local installation)

You will also need to create the database and user/password prior to installation. The installation package can be downloaded from the site, or if you're installing to a remote server, there is a separate link on the Installation page entitled Install With Only FTP Access which is the right method for you.

# Default Installation

There are several features that are activated by default:

+   1. **Games:** Allows users to play games on your site and keeps track of game stats.
+   2. **Categories:** Manages categories that any module can be classified into.
+   3. **Calendars:** Allows users to view calendars with events.
+   4. **MyTiki:** Gives logged-in users their own interface with features such as calendars, webmail, menus, and a notepad, and allows admin to turn user features on or off.
+   5. **Submission:** Allows users to submit articles.
+   6. **AutoLinks:** Allows URLs typed in to text to be automatically submitted to the links directory.
+   7. **Search & Full-text Search:** Allows users to search your site.
+   8. **HTML Pages:** Manages editable blocks of HTML code to be reused throughout the site.