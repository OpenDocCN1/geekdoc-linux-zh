
## Chapter 12: FastTrack Configuration and Administration

- Character set: A style includes the definition of which character set is used to display documents in this directory. The character set can be identified by the browser to correctly display documents in many different languages.

- Document footer: A footer can be added to every document in a directory that a style applies to. A footer is defined and added automatically by the Web server when any document in this directory is sent to a browser.

- Error responses: A style can specify how error responses are handled for documents within a directory. Obviously, documents that are not found on the server do not use the error responses defined for a specific directory ("The Entire Server" setting is System Settings:Error Responses). Error responses for a style might define something like a message regarding user authentication required to access your client directory.

- Log preferences: All accesses to a certain directory can be configured by a style to meet your needs. For example, you might have accesses to a product download logged in a separate file or one division of your organization might prefer that different information be logged for their section of Web pages.

- Remote file manipulation: This feature allows browsers to use the PUT and DELETE features of the HTTP protocol to alter files on your web server. Many browsers don't support these features, and you probably don't want many people to altering your Web pages from their browsers. But if you want to set up these features, the remote file manipulation can be set up for a style to support it.

- Restrict Access: This feature of styles links to the Access Control section, where you can define which hosts and which users can access files in directories that this style is assigned to.

- Server parsed HTML: Server parsed HTML is another name for Server-Side Includes (SSI), which was discussed at length in Chapter 10. Turning on this feature for a style means that all HTML documents in a directory using this style will be parsed by the server before being sent to the browser. This allows SSI commands to be used, but also adds to the processing load on your Web server.

## Assign Styles

The Assign Styles page allows you to apply all the settings defined for a style to a specific document subdirectory on your Web server. None of the features that you define for a style are used by any directory on your Web server until you assign the style to the directory. Settings that you defined for the entire server will also apply to all subdirectories that don't have a style assigned to them.

## Linux Web Server Toolkit

To assign a style, just select a style from the drop-down list of styles and enter a URL in the URL field provided. Press OK to complete your assignment. You can list all the assignments currently in use on your server by using the next page, List Assignments. Each URL and corresponding style name are listed. Assigning a style is like using the <DIRECTORY> contains in the access.conf file for Apache or other web servers. It's a little different in its application, because all the features are contained in a style with a name you select, instead of just listed under the directory where you want them to apply. But that is the same.

![](img/e01f1106dd2902613fa07890c8baa7e6_371_0.png)

Figure 12-16: The Edit Style page lets you select the different features available for a style and jump to where that feature is configured in other sections of the Administration pages.

## Chapter 12: FastTrack Configuration and Administration

345

## Managing Content

The Content Management pages are a collection of many things that allow you to define how your documents on your Web server are handled. Most will be familiar to you from previous discussions of styles, the Apache Web server, or scripting.

## Primary Document Directory

The Primary Document Directory page lets define the document root for your Web server. All URLs requested by browsers will use the directory that you enter as its root. The default document root is /home/httpd/html. You can change this if you need to.

## Additional Document Directories

Every URL that a browser requests is assumed to be under the document root (defined in the Primary Document Directory page). You can, however, place documents anywhere on your Linux system, and by using an alias that makes files available within your document directory root or a subdirectory of it, enable browsers to access them.

Aliases can be assigned in the URL field by entering a URL that a browser request (the alias) followed by a directory on your Web server that the URL should be mapped to (what the alias points to).

For example, suppose you have a file stored on your Linux system as /programs/stocks/chart.html. You want to leave that file in place because local users and programs expect it in that location. But you also want that file to be available on your Web site when users request the URL http://server1.com/stocks/chart.html. Normally, this URL would return the file that is located at /home/httpd/stocks/chart.html. But you can use an alias in the Additional Document Directories pages to point the URL ending in /stocks/ to a different local directory. The entries for this example are shown in Figure 12-17.

![](img/e01f1106dd2902613fa07890c8baa7e6_372_0.png)

Using additional document directories (aliases) presents some security issues because it allows access (albeit not transparently) to areas of your Web server other than the document root, /home/httpd/html.

All of the additional document directories that you define can be assigned a style, so that when documents are from those directories, they are logged in a specific way, or have specific security settings, or a footer text, and so forth. To use a style for the additional directories that you define, just select one from the drop-down list in the Additional Document Directories page.

## Linux Web Server Toolkit

All of the additional document directories that you've assigned are listed at the bottom of this page. The FastTrack Server isn't arranged for you to have a lot of aliases, and you really shouldn't, because of the security issues it raises, and because of how difficult it is to maintain these directories.

![](img/e01f1106dd2902613fa07890c8baa7e6_373_0.png)

Figure 12-17: You can use an alias in the Additional Document Directories to define a URL that retrieves a document from a directory other than your document root or its subdirectories.

## Chapter 12: FastTrack Configuration and Administration

## User Document Directories

User document directories allow each user on your Linux system to have a personal area on the organization's Web server. These user directories are accessed using a special type of alias.

The standard alias for user directories is the tilde character (~), followed by the username. The default directory name within the user's home directory is public_html. For example, if you request this URL:

```
http://www.server1.com/~nwells
```

The Web server would reply with the file /home/nwells/public_html/index.html. You can use the User Document Directories to define which character in a URL defines a tilde (~), but you can choose something else to make your less obviously pointing to user directories. One of your users may appreciate this. On the other hand, don't use a character that occurs at the beginning of other directories, or risk confusing the Web server or making some of your document directories inaccessible.

You can also define which directory within a user's home directory is used to hold the personal Web Pages. Which directory you doesn't really matter, so long as all users are aware of what it is.

For example, if you change the default character to an "at" sign (@) and the directory name to home_page, then this URL

```
http://www.server1.com/@nwells/family.html
```

With additional document directories, user directories (as a group) can be assigned a style so that when documents are sent from those directories, they are logged in a specific way, or have specific security settings, or a specific footer text, and so forth. To use a style for all user directories, just select one from the drop-down list in this page.

## Remote File Manipulation

The Remote File Manipulation page lets a style permit a browser to alter files on your Web server. Remote file manipulation is done through the PUT and DELETE actions that the Web protocol, HTTP, provides. Most browsers haven't implemented these features, and most users would never think of using them. But they do provide a powerful method of distributed computing, particularly for an intranet.

You should have a definite plan for how you expect file manipulation to be used on your Web server, and you should probably include per-user access control for all directories that you assign a style to remote manipulation enabled.
