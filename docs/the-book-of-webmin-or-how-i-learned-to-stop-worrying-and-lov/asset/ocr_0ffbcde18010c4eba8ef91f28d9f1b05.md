Clicking a server icon will simply direct your browser to the Webmin port on the selected server, allowing you to log in. You may also configure Webmin to connect you to the server through a proxied connection, if you provide a user name and password for the other server. This can be useful when connecting remotely to a front-end Webmin server on the routable Internet that also connects to a non-routable private network, allowing an administrator outside of the private network to tunnel through to administer systems inside the private network.

Versions of Webmin beyond 0.85 provide support for some functions to be executable via remote procedure calls, if login information is provided for the remote server. This allows a single Webmin server to directly configure or monitor other Webmin servers. Currently this functionality is limited to the System and Server Status module and some of the modules in the Cluster category. It is likely that many of the other modules will expand to take advantage of this new functionality in the future.

# Webmin Users

This page allows you to configure any number of users and give each some specified subset of the system to maintain. It would allow you, for example, to create a mail administrator who only had access to the Sendmail module, a DNS administrator who could only modify the DNS records, and a Squid administrator who only had permission to edit the Squid configuration. In this way, delegation of authority is very simply and securely handled.

# Editing a Webmin User

To edit a Webmin user and the modules they have access to, click the name of the user on the Webmin Users index page. Each user has a list of accessible modules and a number of additional options that can be configured. From the Edit Webmin User page, it is possible to change the user's password: Select an SSL certificate for them to use for authentication, alter the language and theme from the default and specify the IP addresses from which this user can log in. Also on this page is a list of all modules that are installed on the machine, each with a check box beside it. If checked, the user will have access to the module.

Webmin also allows finer grained control over many modules, and this functionality is becoming more flexible with every release (Figure 3-3). For example, a user with permission to use the Apache module can be denied the ability to edit some specific aspects of the configuration. In the example below you can see that the user is being granted permission to edit only one of the many available virtual servers. To edit fine grained access controls, browse to the Webmin Users index page, and click the module name link beside the user whose access controls you wish to edit.

# Creating Webmin Users

Creating new users is also easy. Click the Create a new Webmin User link and choose a user name or use one of an existing user on the system (Figure 3-4). Choose between using the user's UNIX password or using a new one. Select