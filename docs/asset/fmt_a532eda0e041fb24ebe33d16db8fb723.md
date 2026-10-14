
这将创建一个目录，允许匿名用户放置文件，但他们无法列出他们上传的文件。知道传入目录中文件名称的用户仍然能够下载它，但他们无法列出目录的内容。

您可以对匿名用户施加许多选项和限制来控制对站点的访问，包括控制并发用户数量和他们来自何处。`Ftpd`还有许多选项可以记录所有进出内容。要利用这些功能，请阅读`ftpd`的手册文档。(`rpm -qd wu-ftpd`以查看所有文档的列表及其安装位置。)

Products | Contact Us | About Us | Privacy | Ad Info | Home

Use of this site is subject to certain Terms & Conditions. Copyright © 1996-2000 EarthWeb Inc.
All rights reserved. Reproduction whole or in part in any form or medium without express written permission of EarthWeb is prohibited.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

To access the contents, click the chapter and section titles.

Search this book:

## HTTP

HTTP stands for Hypertext Transfer Protocol. This is the protocol that drives the Web. When you load a file into your Web browser, you are using HTTP. HTTP provides a very secure way of publishing information for others to see. If you want to share information, your Linux system is more than capable of serving to thousands of users.

There are many popular Web servers that run on a variety of systems. By far, the most popular is Apache. Apache is a freely available Web server software distributed under the GNU Public License. Apache powers about 50% of all Web servers on the Internet. If that figure doesn’t seem high to you, consider that the second most popular server is Microsoft’s Internet Information Server, which only absorbs 22% of the market. Netscape servers follow at 8%, and the rest of the server software is under 2% and powers less than 1% of the sites. These statistics are based on more than 3 million Web sites (see www.netcraft.com). Apache is very good indeed. Your system already has it running, even if you didn’t know it.

## Configuring an Apache Server

Apache’s default configuration, as installed, is fairly adequate and secure. If you need to tinker and you are maintaining a public Web server, you should really take a look at a book on Apache. A good one is my book The Apache Server Survival Guide, ISBN: 1-57521-175-0. It covers all the topics that you need to know about setting up and maintaining an Internet server. It doesn’t assume much but provides in-depth information and many examples. It also orients you on HTML and CGI programming.

Apache’s configuration files can be found at `/etc/httpd/apache/conf`. Configuration of an Apache server is done in three text files: `httpd.conf`, `access.conf`, and `srm.conf`. Configuration for Apache is straightforward. Directives appear one per line. The first word on the line is the directive; the rest are the parameters or configuration settings. Fire up your editor and open `/etc/httpd/apache/conf/httpd.conf` to see what I am talking about. You’ll see the following:

- The `httpd.conf` file is the primary Web server configuration file. This file sets the default behavior of the server, such as its name, the port it runs under, the location of configuration, logs, and error files. Without getting into the depths of it, here is the only directive that you need to change in this file:
  - `ServerName`—This should reflect a valid DNS name for your system. If you don’t know the fully qualified DNS name for your system, leave this as `localhost`.
- The `srm.conf` configuration file keeps track of where information published by the Web server resides. It also provides a mapping between icons and files that the Web server uses when generating automatic file indexes. There are two directives that are important for you to know about:
  - `DocumentRoot`—This directive specifies where your HTML documents are found. By default on Linux, this points to `/home/httpd/html`. This directory contains HTML help Linux documentation pages (if you are running Caldera’s distribution) or the Apache Server documentation.
  - `UserDir`—This directive specifies the name of a directory users can create in their accounts. Files in this directory are accessible using a browser and a URL such as `http://servername/~username/` (note the tilde (`~`) before the username).
  - `DirectoryIndex`—This directive specifies the name of files that will be loaded when a user requests a directory instead of an HTML file. If you take a look at the URL in the preceding item (`http://servername/~username/`), this URL doesn’t request a file, it requests a directory. (This is similar to when you request `http://www.caldera.com`; this is just the name of a machine!). This directive specifies a filename to search when incomplete URLs are specified; if the file is found, it is sent to the browser. Otherwise, the server will generate an automatic server index, listing all files contained in the directory. You can define multiple `DirectoryIndex` files like this:
```
