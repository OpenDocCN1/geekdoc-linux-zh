
# Linux Web Server Toolkit

> Web server configuration is described in Chapters 11 and 12. If you're using the Apache Web server (the default in OpenLinux Lite), server-side includes are enabled using the Options Includes directive in the access.conf file.

This capability allows you to easily configure your HTML files in all sorts of powerful ways.

# Using Common Server-Side Includes

There are numerous standard server-side includes that can be included in your HTML files, with additional commands available by modules or APIs with your Web server. The examples in this section show the most commonly used commands: Note that each one uses the following format:

```
<! server_side_command an_attribute= the_value_of_the_attribute
```

The most commonly used command and the easiest to explain is the #include command.

The #include command inserts another file into the HTML file. The next example might be used to include a footer in every document. When the footer changes, the footer.html file can be changed, without the need to alter every file individually. Any file can be included using an #include command, even a text file, as follows:

```
<! include virtual=footer.html
```

The #exec command, shown in the next example, allows you to include the output of a system command or script into your HTML document. If the attribute is used with #exec cmd, you can include a system command (a directory listing in the example); if the attribute used with #exec cgi, you can include the name of a script — there are two examples shown here because of the different ways the output might be captured by the Web server — as follows:

```
<! exec cmd=ls -l
<! exec cgi= welcome.pl
```

The #echo command is like using echo at your command line to determine the value of an environment variable. The var value is the name of any environment variable that is visible to the Web server. This includes the current date and any values that were passed from forms on the browser, though it's not common to combine a form with an SSI document because you would use a script to process the form data. The following is an example of the #echo command:

```
<! echo var= LAST_MODIFIED
```

# Chapter 10: Basic Scripting and Forms

Variables that can be used with #echo include those listed in Table 10-1.

# Table 10-1 System Variables That Can Be Used as Values with the #echo Command

| Variable | Description |
| --- | --- |
| LAST_MODIFIED | The date the HTML file was modified. (Very useful for placing a "last modified" line at the bottom of HTML documents to inform users how up-to-date your site is.) |
| DOCUMENT_NAME | The filename of the HTML file for the SSI command is in. |
| DOCUMENT_URI | The complete path of the HTML file that the SSI command is in. |
| DATE_LOCAL | The current date and time (local time zone). |
| DATE_GMT | The current date and time (Greenwich Mean Time zone). |

You can use separate commands to get the file size or last modified date without using the #exec or #echo commands, as shown in the following two examples:

```
<! fsize virtual= toc.html >
<! #lastmod virtual= toc.html >
```

The first line will insert the file size of the file toc.html. The second line will insert the last modified date of the file toc.html. Note that the #lastmod command can be used to insert the last modified date of any file, while the #echo command can be used only to insert the last modified date of the file containing the SSI command.

In addition to these a few other commands that insert information into your HTML document, there are a few special commands that configure how your information is displayed.
In the #echo example above, suppose you used the DATE_LOCAL variable, but you didn't like the standard format that it was displayed in or you want to insert the file size for a file, but it's large, so you want it in megabytes instead of bytes.
The #config command can do these things for you. It can use attributes like sizefmt and timefmt to determine exactly how the data inserted into an HTML file will be displayed. You use the #config command first in a file where other commands are used later. The following are two examples:

```
<! #config sizefmt= abbrevi >
<! #config timefmt=%d/%m/%Y >
```

# Linux Web Server Toolkit

These #config commands would cause a #size command that occurs later in the same document to print the file size in kilobytes or megabytes, depending on its size, instead of bytes. They would also cause an #lastmod command or an #echo command with LAST_MODIFIED to use the altered format for displaying the date. The parameters for date and time format can be reviewed by entering help at a command line.

# Drawbacks of Server-Side Includes

Server-side includes are a powerful tool for some needs that you may have with your documents. They are often not used, because of two issues.

The first issue is that server-side includes places a large burden on the Web server. The Web server must review every line of every file that it sends out, the throughput for busy Web sites can be reduced substantially if server-side includes are turned on.

There are a couple of solutions to this problem. Much of the functionality provided by server-side includes can be created using other types of scripts that review your file during slow traffic times, inserting changes as were the last modified.

> TIP If you see a real need for server-side includes to make your Web pages appear as you want them to, you can compensate by having greater CPU and memory capacity to handle the load.

One key to using server-side includes is effectively to activate them only in the directories where they are actually used. This means you'll need to list them as an active option for a specific directory in the access.conf file or similar for your Web server (this is discussed further in Chapters 11 and 12). If server-side includes are not listed as an option for your main document directory but are available for a smaller subid where many of the documents use SSI, the load on your Web server will be considerably less, because only documents requested from the small subid need to be parsed for SSI commands.

The second issue when using SSI is the security problems it can pose. In particular, the #exec command presents a grave danger, for both the data it can send to users and the damage it can do on the Web server.

For example, using the command #exec cmd= /etc/passwd will include your password file in an HTML document. And the command #exec cmd= rm -rf /* will delete every file on your Linux server. Passing file data to users is a common danger. Destroying data on your Web server is easy to prevent by configuring the Web server to run as a user no access rights.

# Chapter 10: Basic Scripting and Forms

This danger is less of a concern if only trusted users are creating Web pages on your site, but someone may not know the security holes they are causing or what to watch for if a malicious “friend” gives them an updated page that is posted without careful review.

In order to remove this danger while still providing the usefulness of SSI commands, Web servers allow you to specify that other SSI commands can be used, but not the #exec command. In Apache, the default OpenLinux Lite server, is this inside the access.conf file (this is described in more detail in Chapter 11). Instead of the following standard line:

```
<Directory /home/httpd/html/special/files/>
Options Includes
</Directory>
```

which allows all SSI commands within the named directory, you can use the following command:

```
<Directory /home/httpd/html/special/files/>
Options IncludesEXEC
</Directory>
```

which allows all SSI commands except the #exec command to be used within the named directory. The next section describes how to create HTML forms that gather the data on which Web server scripts operate.

# Creating HTML Forms

HTML forms provide an easy way to make your Web pages interactive. They’re used on a large percentage of Web sites for entering customer information, search queries, or other data that the Web server uses to customize a response for the user.

Creating HTML forms is very easy. When you think about it, the elements you normally see in a graphical user interface are very few in number. HTML tags tell the browser to display each of these interface elements. The page is then displayed in a way that allows the user to enter data that the browser sends back to the Web server.

The great thing about using a Web server with HTML forms is that the browser always displays the interface elements in the form just as they appear in all applications on that platform. For example, a form that is displayed in a Linux browser looks like the one in Figure 10–2, matching the interface style of the X Window System.
