
## WordPress

WordPress is a great “out of the box” blogging package that provides excellent customizability and functionality. It is available at http://www.wordpress.org and the current version at time of this writing is 1.5.11.

### Installation Notes

Installation of this package is incredibly easy and quick to do. Prior to installation, make sure you are running PHP 4.1+ and MySQL 3.23.23+ and that you have created your database and username/password. The rest of the documentation you would need is conveniently located for you on the http://www.wordpress.org site.

### General Overview of Features

WordPress offers numerous functions and areas of customization for your blog, including:

- **User registration system**: Allows you to authorize other users to post, edit, and delete blogs in your site, with 10 levels of varying user access. You can also require an “approval” process before drafts are published.
- **Static content pages**: Allows you add static pages to your site, and manage them through the WordPress interface.
- **Adding links or blogrolls**: You can manage and organize external links through the WordPress interface.
- **Themes**: There are currently 35 themes built-in to the default installation and nearly 150 additional themes available for you through download to easily customize the look and feel of your blog.
- **Comment system**: Allows you to accept, review, and modify comments posted by users and contains a spam blocker to prevent spam posts from popping up. Visitors can also make comments about your blog on their own sites through Trackback and Pingback.
- **Hidden posts**: Allow you to password-protect certain posts that are viewable only by you, or by the author who created them.
- **Importing data**: Allows you to import data from other popular blog packages including MovableType, Blogger, and numerous others.
- **RSS feed**: Allows others to syndicate your blog.
- **Post-by-email**: Allows you to submit blog posts through the email system.

There are other nice features with this blogging package such as full standards compliance, ease in upgrading, and the use of the Texturize engine to beautify your text from plain ASCII.

### Summing It Up

You will find once you delve into the WordPress package that it is well documented, easy to install, easy to configure and customize, and very functional. It also has an excellent support and development community in case you have questions or problems. If you are simply looking to create a blog on your site, WordPress is hard to beat.

## Serendipity

Another fabulous and well-structured blog is Serendipity, available for download at http://www.s9y.org. It boasts some heavy PHP hitters on its development team, including Sterling Hughes, George Schlossnagle, Wez Furlong, and Sebastian Bergmann, among others. It is also the blog package of choice for many core PHP developers.

### Installation Notes

Like Wordpress, installation is a quick and easy job. You should be running PHP 4 or greater and MySQL, PostgreSQL, or SQLite for your database. The only other thing to keep in mind is to remember to restrict the file permissions after installation, as outlined in their extensive installation documentation found at http://www.s9y.org/index.php?node=36.

### General Overview of Features

Serendipity offers similar functionality to Wordpress, such as allowing the admin to set permissions for users so that not all users can publish blog entries, and moderating comments or enabling CAPTCHAs for spam prevention. With Serendipity, you can add images to your blog posts, change themes for your site, import and export data, and offer trackback and pingback for others to reference your posts. Also akin to Wordpress is the standards compliant code and RSS feeds that can be offered for others.

Some additional functionality not readily seen in Wordpress includes:

- Optional Wysiwyg editors: HTMLArea, FCKeditor, xinha, TinyMCE
- MySQL, PostgreSQL and SQLite support
- Multiuser blogs: One installation of serendipity can serve independent weblogs.

### Summing It Up

Serendipity is simple, clean, and solid. If you're looking for a blog that simply does what it's supposed to do and is very reliable, Serendipity is an excellent choice.

## Wiki

Just as programmers, coders, and web developers alike use software to manage development and deployment of software packages, they are turning to wiki to collaborate and create comprehensive documentation to complement those packages.

### The Origin of Wiki

According to Wikipedia, the word *wiki* is based on a Hawaiian term, *wiki wiki*, meaning “quick or informal,” specifically when referring to the buses at the Honolulu airport. The phrase was coined by Howard (“Ward”) Cunningham back in 1995 as a reference to the Portland Pattern Repository, a collaboration of software development ideas.

As the Internet has grown to reach the masses, the popularity of the wiki concept has grown substantially, particularly in the open source community where many people assume a community responsibility to continually improve existing products. Documentation is an integral part of enabling users to understand what an application does or can do.

Wiki sites are not only limited to supporting open source projects, but can also act as a general reference guide for virtually anything. There are hobby-oriented wikis, language wikis, gaming wikis — you could conceivably create a wiki for any topic under the sun.

### MediaWiki

One of the more popular packages available, and the brains behind Wikipedia, is MediaWiki. It is available at `http://wikipedia.sourceforge.net`. The latest release at the time of this writing is 1.4.4 and will be the focus of the discussion here.

#### Installation Notes

Prior to installing MediaWiki, you should take note of the following: If you have root access, you will not need to create the database pre-installation. If you are installing on a remote server, you will need to create the database yourself before installing. Also, after the files have been unzipped, you will need to `chmod` the config directory so that it is writable. You will also need to reset the permissions upon completion of installation.

The complete installation guide can be found at the MediaWiki Web site: `http://meta.wikimedia.org/wiki/MediaWiki_User%27s_Guide:_Installation`.

#### General Overview of Features

Because the purpose of the site is to keep track of a continually evolving body of text, it has some wonderful features for managing users, their input, and version control. General functions available are:

- **User customization and access**: Users can customize their own time interface by editing their own templates, setting their own preferences for things such as time zone and number of results per page. Admins can assign varying levels of permissions to user groups, turning on and off the ability for them to edit, move, contribute, or upload files, among other things.
- **Search capabilities**: Visitors to the site can perform a full-text search of all the articles contained on the site.
- **Reports**: Reports can be generated that provide specific statistics on usage, articles and links, article activity and popularity, images, users, and more.
- **Editing articles**: Users can decide to edit only a portion of an article, articles can be merged if an edit conflict occurs, users can preview their edits before submitting them, and users are given the use of an editing toolbar to facilitate the editing process.
- **Article organization**: Articles can be categorized and subcategorized into unlimited categories.
- **Text and linking control**: Users can use restricted or full HTML code when submitting text changes or entering new text. Embedded hyperlinks can also be managed.
- **Watchlist**: This feature assists the admin and users in keeping track of users' edits and contributions. It can show articles of particular interest, recent changes, and which users have contributed the most. This feature even offers a side-by-side view of the article pre- and post-edit with the changes highlighted so changes can be easily identified by the reader.

![](img/fd2e7361878181c2b12e30301ff3e182_350_0.png)
