# 666

# Part V ✦ Running Servers

"File not found" errors can be checked in the same way as access forbidden and server internal errors. You sometimes find that Apache is not looking where you think it for a specific file. Generally, the entire path to the file shows up in the error log. Make sure you are accessing the correct virtual host, and check for any Alias settings that might be directing your location to a place you don't expect.

+   File permissions — A "file permissions prevent access" error indicates that the apache process is running as a user that is unable to open the requested file. Make sure that the account executes permissions on the directory and every directory above it, as well as permissions on the files themselves. Read permissions on a directory are also necessary if you want Apache to generate an index of files. See the manual page for chmod for more information about how to view and change permissions.

Read permissions are not necessary for compiled binaries, such as those written in C or C++, but can be safely added unless there is a need to keep the contents of the program secret.

+   Access denied — A "client denied by server configuration" error indicates that Apache was configured to deny access to the object. Configure the configuration for <Location> and <Directory> sections that might affect the file you are trying to access, remembering that settings applied to a path are also applied to any paths below it. You can override these by changing the permissions only for the specific path to which you want to allow access.

+   Index not found — The "Directory index forbidden by rule" error indicates that Apache could not find an index file with a name specified in the DirectoryIndex directive and was to create an index containing a list of files in a directory. Make sure your index page, if you have one of the names specified in the relevant DirectoryIndex directive, add an Options Indexes line to the appropriate <Directory> or <Location> section for that object.

+   Script crashed — "Premature end of script headers" error can indicate that a script is crashing before it finishes. Sometimes, the errors that caused this also show up in the error log. When using exec or suPHP, this error may also be caused by a file ownership or permissions error. These errors are indicated in /var/log/apache/suex.log or /var/log/apache/suphph.log.

# Securing Your Web Traffic with SSL/TLS

You add security for your server, using your own certificates. Your certificate is important, and so is your capability to pass it along your network or the Internet to others. Networks aren't secure enough by themselves to protect your communications. This section examines ways in which you can guard your communications.