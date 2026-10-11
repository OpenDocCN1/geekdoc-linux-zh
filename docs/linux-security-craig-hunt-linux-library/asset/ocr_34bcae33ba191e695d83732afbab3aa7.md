# # In Sum

Samba provides a number of configuration parameters that allow you to run a tight installation, but, as always, the devil is in the details. You should start by protecting the SWAT management tool with SSL in order to avoid unnecessary exposure of your configuration to eavesdropping attack.

Next, you need to decide what type of authentication you are going to use, based on the nature of shares that you'll be offering and the identity of your user population. If you need to make shares available to guest users, `share mode authentication` is the only feasible alternative. If your user population is known and trusted and you know their user names a priori, `user mode authentication` is a better option.

Access control can play a fundamental role in the security of your Samba server. Make use of the `valid users` directive to restrict shares to only those users who should be granted access to specific files within your Linux server. If you are integrating a Samba server into an existing Windows NT domain, you may want to consider `server` or `domain` mode authentication to leverage the user databases that already exist on your domain controller. Alternatively, Samba itself can be configured to be your primary domain controller.

Finally, if your users will be accessing remote Samba servers, you should be concerned about the privacy of your SMB traffic because it traverses the Internet backbone. OpenSSL can be used in conjunction with the SSL Proxy package to protect Samba communications using the Secure Sockets Layer.

This chapter wraps up the discussion of security for applications. The next chapter, “Network Layer Firewalls,” kicks off Part 4 of this book, “Perimeter Security,” dedicated to firewalls and other perimeter defense applications.