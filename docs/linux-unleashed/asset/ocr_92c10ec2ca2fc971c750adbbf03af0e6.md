When it is selected by the user, the program stats.cgi on the Web server www.tpci.com is located and run. This might be across the country—it doesn't matter to either HTML or CGI, as long as the reference can be resolved.

Three kinds of methods are usually used to call a CGI application: the GET, HEAD, and POST methods (all are part of HTTP). They differ slightly in when you use them. We can look at each briefly so you know what they do and when they are used.

A **GET method is used when the CGI application is to receive data in an environment variable called QUERY_STRING**. The application reads this variable and decodes it, interpreting what it needs to perform its actions. The GET method is usually used when the CGI application has to take information but doesn't change anything.

The **HEAD method** is much the same as the GET method, except the server only transmits HTTP headers to the client. Any information in the body of the message is ignored. This can be useful when you need to handle only a user ID, for example.

The POST method is much more flexible and uses stdin (standard input) to receive data. A variable called CONTENT_LENGTH tells the application how much of the data coming into the standard input is important so it knows when all the data has arrived. The POST method was developed to allow changes to the server, but many programmers use POST for almost every task to avoid truncation of URLs that can occur with GET.

A number of environment variables are used by CGI, most of which are covered in much greater detail in CGI programming books. Describing all the variables here without showing you how to use them would be a bit of a waste.

# # CGI and Perl

If you do get into CGI programming, you will probably find that most of it is done in the Perl programming language (which we looked at in Chapter 28, "Perl"). CGI programming can be done in any language (and many Web page designers like C, C++, or Visual Basic because they are more familiar with those languages), but Perl seems to have become a favorite among UNIX Web programmers.

The reasons for Perl's popularity are easy to understand when you know the language: It's powerful, quite simple, and easy to work with. Perl is also portable, which lets you develop CGI programs on one machine and move them without change to another platform.

There are a lot of Perl CGI scripts to be found on the Web. A quick look with a search engine such as AltaVista will usually show hundreds of examples that can be downloaded and studied. For example, one of the most commonly used Perl scripts is called GuestBook. Its role is to allow users of your Web site to sign into a guest book and leave