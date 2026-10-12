Following is an alphabetical list of those modules that are included with Red Hat's Apache RPM.

# mod_access

This module gives you the ability to control access to areas on your Web server based on IP addresses, hostnames, and/or environment variables. You will be able to grant or deny access to any part of your Web server depending on those criteria. It is possible to use partial hostnames or subsets of IP addresses as access qualifiers. For example, you might want to allow anyone from within your own domain to access certain areas of your Web. See the section “Authentication and Access Control” for more information.

# mod_actions

This module provides the ability to dynamically execute scripts based on the type of HTTP request. You will be able to map the execution of CGI scripts to MIME content types or request methods.

# mod_alias

There are times when you need to manipulate the URLs of incoming HTTP requests. You might want to redirect the client’s request to another URL, or you may want to map a part of the filesystem into your Web hierarchy. For example:

Alias /images/ /home/wwb/graphics/

This example would fetch contents from the /home/wwb/graphics directory for any URL that starts with /images/. This will be done without the client knowing anything about it. If you use a redirection, the client will be instructed to go to another URL to find the requested content.

For more advanced URL manipulation, look at mod_rewrite also.

# mod_asis

Using this module you will be able to specify in fine detail all information that is to be included in a response. This will completely bypass any headers that Apache might otherwise have added to the response. All files with an .asis extension will be sent straight through to the client without any changes.

As a short example, assume that you have moved the contents from one location to another on your site. Now you need to inform people who try to access this resource that it has moved, as well as redirect them to the new location automatically. To do this you might add something like the following code into a file with an .asis extension.

![](bbox=[0.88, 0.25, 0.98, 0.4])