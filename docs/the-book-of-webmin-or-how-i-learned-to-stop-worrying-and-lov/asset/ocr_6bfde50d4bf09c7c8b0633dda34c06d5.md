![](bbox=[0.22, 0.1, 0.78, 0.38])

Figure 9-3: Messages and Banners

# README files

Here, you can configure the behavior of the server with regard to README files. This, too, is set up by default on most systems. In this case, any file beginning README will be displayed to the user, both on logging into the server, and upon entering a new directory. This option configures the readme directive.

# Greeting level

Here you can select how much information about your server will be presented to the user. This can include the host name, the server version, and nothing. This can be a mild security risk, as the first step to cracking a box is to figure out what software and version is running. However, if the system is kept up to date (religiously), and the system is otherwise secured, this should not be an issue. Many paranoid types (and there’s no harm in being paranoid in a world where script kiddies are a dime a dozen) will disable all specific software and version information on all of their publicly accessible services. This option configures the greeting directive.

# Pre-login banner

Here you configure a banner that will be displayed before the user is prompted for a user name and password. This option can cause problems with non-compliant FTP client software. This option configures the banner directive.

# Hostname for messages

This will be the host name that is printed in the greeting message, and anytime the host name is inserted into a message for the user. This option configures the hostname directive.