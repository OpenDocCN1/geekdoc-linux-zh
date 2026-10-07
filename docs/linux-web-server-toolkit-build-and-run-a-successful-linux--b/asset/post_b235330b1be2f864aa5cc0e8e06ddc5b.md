
# Linux Web Server Toolkit

# Document Preferences

The Document Preferences page appears to be a catch-all where Netscape stored several seemingly unrelated items on document management. The page is shown in Figure 12-18.

![](img/e01f1106dd2902613fa07890c8baa7e6_375_0.png)

Figure 12-18: The Document Preferences page lets you a variety of options for how documents are used on your Web server. Options include how directories are indexed and which file is used as your Home Page.

# Chapter 12: FastTrack Configuration and Administration

The Index filename field defines which filenames are used as default documents when someone uses a directory name in a URL. In truth, URLs that people enter are directories, not filenames. The Web server can return a default file from that directory or return a list of the files that are in that directory.

The first option is more common and more security conscious. The default file that is usually returned is index.html. So, for example, if a user requests this URL:
http://www.server1.com/documents/

The web server tries to find the index.html file in the documents directory, and returns it to the browser. The Index Filenames field defines which filenames are searched in the case that the user does not specify a filename.

You can also set what should occur if no file is found with the filename defined as the index filename. I just mentioned that the Web server can generate an index (file listing) of the directory. If you don't want the user to see a listing of the directory contents, the Directory Indexing option on this page lets you determine what is sent: You can send a "Fancy" index, which includes icons and descriptions of files based on their type; a "Simple" index, which includes only filenames and sizes; or not (the "None" index, which prevents a security issue by returning "File Not Found" if the URL requested only indicates a directory where No Index file is available).

Almost all Web sites start at the document root with the index.html file. But you can define another document file as your home page in FastTrack. This will be the default file if a browser requests only the root directory from your server. To use this feature, just enter a filename in the Home Page file.

Finally, your Web server needs to know what documents are made when it sends them to a browser. This tells the browser how to display the document. The MIME types defined on your server take care of this in most cases, but the Web server needs a default, so that files cannot be assigned another type have some normally plaintext or ASCII text. You can change this if you prefer, to something like HTML, or something else that occurs in your MIME types file. I recommend leaving this unchanged.

# URL Forwarding

One of the error codes that a Web server can generate is a "Document Moved" message. Many browsers can immediately recognize when this message is sent, and we will retrieve the document from the new location without telling the user that the original URL wasn't valid.

If you change the location of a popular document on your Web site, or you can automatically send a "forwarded" message to the browser so that the Web page is still retrieved from the new location.

To do this, enter a URL (in the URL field) for the document on your Web server that has moved (this is the URL that a user might enter in her browser). Then enter the new URL location of document. If the document moved to a new directory on your Web server, enter the new directory in the URL Prefix field; if the document moved to another Web server, enter the complete new URL in the Fixed URL field.

All of the forwarding orders that are in effect on your site are listed at the bottom of the URL Forwarding page. You can edit or remove any that have changed or are old. It's OK to leave forwarding orders in place for several months. They don't hurt your server performance and they provide a great service for users that want to reach something other on your system because they knew it previously.

> When you create a forwarding order, be certain that the document that you forward to remains valid.

![](img/e01f1106dd2902613fa07890c8baa7e6_377_0.png)

# Software Virtual Servers

FastTrack Server allows you to serve documents on the Web as if they were coming from another domain name, but actually have them located on the same physical computer. This is often called a multi-domain Web server; it's part of the Apache Web server as well.

You must set up your IP routing and DNS configuration files to permit traffic for several names to come to the same computer. You can also set multiple copies of FastTrack Server to handle these multiple domain names. But if the administration of the domain names is very similar (such as for divisions of a company), it's easier to set up multiple domains within a single copy of FastTrack instead of starting multiple copies of FastTrack.

These are called virtual servers because you're not really starting another server program (http daemon), you're just making it look like you have more than one Web server running on this machine because you're servicing multiple domains. But actually you have only a virtual server, running in software.

The appearance of multiple, virtual Web servers is managed from the Software Virtual pages by entering two things:

- The URL (containing a new domain name) that will be used for the new virtual server
- The file to use as a home page document for requests to the new URL that you entered

# International Characters

Most Web browsers can display pages in many languages. Most languages other than English you might be familiar with, use at least some special characters.

# Chapter 12: FastTrack Configuration and Administration

FastTrack can use a style setting to define the character set for documents within a directory. The name of the character set is sent to the browser, the browser then knows how to correctly display the document. Most Web browsers can display pages in many languages. Most languages other than English you might be familiar with, use at least some special characters.

# Document Footer

Styles that you define and assign to subdirectories can include an automatic footer. The footer is added to the end of every document sent from a directory that has this feature enabled. Footers are very short, with something like:
- An email address
- Date modified
- A copyright line

In the Document Footer page, you can select a style to which footer will apply, then define how the footer will look. You can specify how the date string is formatted if you don't like the default. Then just enter the text that should be included in the field shown (as shown in Figure 12-19). You may not want all files in a subdirectory to have the footer enabled. In fact, adding it to all files would include files like GIF graphics and CGI script types, which would cause problems. The standard list of file types to add to the footer is HTML and text files.

# Parsed HTML

Chapter 10 describes at length the use of Server Includes. These are commands that are embedded within HTML tags that look like comments to the browser. The Web server executes these commands to customize a document just as it's being sent to the browser — a sort of real-time editing of the HTML file.

Because this feature poses a security threat (especially with the ability to execute commands on your Linux system), and causes an extra load on your Web server, you can define which directories have this feature enabled. Document directories that do not have this feature enabled via a style definition will not have their files scanned for SSI commands, saving the server's time and making the site a little more secure.

If you want to make a style that you assign to a directory so that the Web server automatically checks every HTML file for SSI commands as it's being sent, just select the Yes button on that page after selecting a style from the dropdown list. You can either select "Yes with Exec," which is an unqualified Yes, or select "Yes without Exec," which indicates that files will be scanned for SSI commands, but the Exec command (which causes the biggest security concern) will be ignored.

Finally, you can define which files in the directory that this style is assigned to will be scanned. It can save a lot of time to restrict this to only .html files, or only files with the execute bit set. Using only the execute bit can save your server a lot of extra processing in going through files that don't even use SSI commands.

![](img/e01f1106dd2902613fa07890c8baa7e6_378_0.png)
