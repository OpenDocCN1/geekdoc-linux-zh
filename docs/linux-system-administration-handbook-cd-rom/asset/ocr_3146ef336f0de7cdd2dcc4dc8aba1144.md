Perl, ignoring, for the most part, C, Python and other languages. C, in particular, is very useful since, as a compiled language, CGI written in it is faster and lighter weight. Of course, development times in C are much longer.

At this point, all of the languages mentioned have more or less equivalent extensions/modules/libraries for dealing with the peculiarities of CGI and interfacing with everything from TCP/IP sockets, the operating system to a database. As such, the choice of a language for CGI is largely up to you. All of the above are shipped with most Linux distributions and are available for free from their respective authors.

# Web Pages for Your Users

In a situation where you have multiple users on your machine, it be at an ISP or at a publisher, some of them will likely be interested in setting up a home page for themselves.

This is not something that will typically consume a large amount of resources on your server unless you have a large number of home pages or have very popular users. Additionally, serving the static HTML poses no security concerns beyond those of running the server itself. All that aside, there will almost certainly be users who will want to use some CGI, SSI, or some other server-parsed content that will add a dynamic element to their Web pages. Now, you have a security issue.

The various solutions range from simply allowing users access to tools like SSI and CGI (in a situation where you trust all your users) to some sort of limited SSI/CGI to completely forbidding the use of them. You can also allow or disallow the use of them on a user-by-user basis.

In a small business or possibly on a corporate LAN, you may likely choose the former route while at an ISP, where you know few of the users personally, you will likely choose one of the latter routes.

Fortunately, Apache controlling access to these and other tools fairly easy via the .htaccess file and <Directory> directive.

# Restricting the Use of CGI and SSI

The <directory> directive is your friend. It is the way you specify what can and can't be done in which directories. Couple this with the Linux user and group permissions, and you can exercise very fine control over who can do in what in areas of your Web space.

In general, unless the server is already so insecure it doesn't matter, or you can trust your users not to inadvertently or purposefully write CGI which