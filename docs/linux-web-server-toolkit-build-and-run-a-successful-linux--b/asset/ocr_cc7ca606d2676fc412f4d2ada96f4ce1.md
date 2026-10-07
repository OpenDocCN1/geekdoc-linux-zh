# Chapter 12: FastTrack Configuration and Administration 349

The Index filename field defines which filenames are used as default documents when someone uses a directory name in a URL. In truth, URLs that people enter are directories, not filenames. The Web server can return a default file from that directory or return a list of the files that are in that directory.

The first option is more common and more security conscious. The default file that is usually returned is index.html. So, for example, if a user requests this URL:
http://www.server1.com/documents/

The web server tries to find the index.html file in the documents directory, and returns it to the browser. The Index Filenames field defines which filenames are searched in the case that the user does not specify a filename.

You can also set what should occur if no file is found with the filename defined as the index filename. I just mentioned that the Web server can generate an index (file listing) of the directory. If you don't want the user to see a listing of the directory contents. The Directory Indexing option on this page lets you determine what is sent: You can send a "Fancy" index, which includes icons and descriptions of files based on their type; a "Simple" index, which includes only filenames and sizes; or not (the "None" index, which prevents a security issue by returning "File Not Found" if the URL requested only indicates a directory where No Index file is available.

Almost all Web sites start at the document root with the index.html file. But you can define another document file as your home page in FastTrack. This will be the default file if a browser requests only the root directory from your server. To use this feature, just enter a filename in the Home Page file.

Finally, your Web server needs to know what documents are made when it sends them to a browser. This tells the browser how to display the document. The MIME types defined on your server take care of this in most cases, but the Web server needs a default, so that files cannot be assigned another type have some normally plaintext or ASCII text. You can change this if you prefer, to something like HTML, or something else that occurs in your MIME types file. I recommend leaving this unchanged.

# URL Forwarding

One of the error codes that a Web server can generate is a "Document Moved" message. Many browsers can immediately recognize when this message is sent, and we will retrieve the document from the new location without telling the user that the original URL wasn't valid.

If you change the location of a popular document on your Web site, or you can automatically send a "forwarded" message to the browser so that the Web page is still retrieved from the new location.

To do this, enter a URL (in the URL field) for the document on your Web server that has moved (this is the URL that a user might enter in her browser). Then enter the new URL location of document. If the document moved to a new directory