# Miscellaneous Options

The following are some of the common tags that can be used to further define how proftpd works:

+   - **AllowRetrieveRestart**—This option, when set to on (default), allows clients to resume interrupted file retrievals. It's recommended that you set this option to on.
+   - **AllowStoreRestart**—This option, when set to on, allows clients to resume interrupted file uploads to the server. We don't recommended that you set it to on because this will allow various users to corrupt existing files. Its default setting is off.
+   - **CDPath**—This is exactly like the shell's CDPATH environment variable. It takes a path as an argument, allowing the user to directly change her working directory to any directory inside that path by just specifying its name. For example, suppose you have a directory called /usr/local and inside it you have /usr/local/files. Setting CDPath to /usr/local/, as in the following:
+   
+   ```
+   CDPath /usr/local/
+   ```
+   
+   will allow any user to change her working directory to /usr/local/files by just typing the following regardless of where that user is currently positioned on the filesystem:
+   
+   ```
+   cd files
+   ```
+   - **DefaultTransferMode**—ftp uses one of two modes of transfer—ASCII for text files and Binary for others. Usually, ftp clients tell the server which one to use, depending on the type of file being transferred. You can tell proftpd which to use by default just in case. The following is an example:
+   
+   ```
+   DefaultTransferMode binary
+   ```
+   - **HiddenStore**—Setting this option to on will cause proftpd to store incoming files as hidden files until the transfer is complete. When the file is fully transferred, proftpd will unhide it. This is useful if you want to ensure that no one attempts to download a file that is still being uploaded to the server.
+   - **HideNoAccess**—Entering this option in your configuration file will tell proftpd to hide any directories that the currently logged in user has no permission to see. What is meant by permission here is the Linux filesystem permission. Because the user will be unable to access the directories anyway, you might as well tell proftpd to hide them using this option. This option applies to <Directory> and <Anonymous> sections.
+   - **MaxLoginAttempts**—This is how many times proftpd will let the user attempt to log in incorrectly before disconnecting him.
+   - **ShowDotFiles**—Setting this option to on will cause proftpd to show hidden dot files.