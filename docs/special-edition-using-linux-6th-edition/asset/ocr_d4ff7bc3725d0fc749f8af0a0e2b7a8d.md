> **Note**
> 
> If you have followed some of the examples in previous chapters of this book (or if you have reinstalled or upgraded the Apache package), you might see configuration files with the extension `.rpmsave`. For a description of how these files are used by the package manager, see Chapter 16, “Software Package Management.” Don’t worry about them for now.

# LOCATION OF LOG FILES

Log files are configured by default to be written in the directory `/usr/local/apache/logs`, though this is often changed by various distributions. Log file options are discussed later in this chapter in the section “All About Logging.”

# DEFAULT DOCUMENT DIRECTORY

The default document directory for Apache is `/usr/local/apache/htdocs`, though this varies among distributions. This means that when you put a file in this directory, or in subdirectories of this directory, remote users can see the file.

Other directories are also configured, by default, to be available through the Web server to the outside world, including the following directories:

+   - `/usr/local/apache/cgi-bin`
+   - `/usr/local/apache/icons`
+   - `public_html` under each user’s home directory (for example, `/home/tim/public_html`)

All these directories appear at different locations in the directory structure (name space) that is visible to the outside world. This is explained in the section “Defining the Document Name Space.”

# TYPES OF CONFIGURATION DIRECTIVES

At this point, before a detailed presentation of server configuration directives, it is useful to categorize the different options for the server.

Table 33.2 showed the different files that are used to hold configuration information for the Web server. The configuration data falls into roughly four major categories (represented by the files mentioned in the table).

There are global server directives, which control aspects of the server such as its address, the user and group account it runs as, and log file formats and locations. Also, there are numerous options for tuning the performance and responsiveness of the server, and for setting timeouts and limits used by the server for its network connections.

Another category of directives has to do with how the server handles requests. The server provides a whole tree of documents to the outside world. Certain directives define this tree, including the location of the main document directory and other directories that the server provides. Furthermore, these directives control how the items in the tree are presented to clients (whether they are returned as files, as directory listings, or as output from programs