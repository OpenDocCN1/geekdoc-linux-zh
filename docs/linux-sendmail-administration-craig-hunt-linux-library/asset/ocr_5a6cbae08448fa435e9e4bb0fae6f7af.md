# Chapter 5 Understanding a Vendor's Configuration

back to Listing 5.3. The last line in the generic.m4 file is the EXPOSED_USER macro. The EXPOSED_USER macro adds usernames to class E. The users listed in class E are not quarantined, even when masquerading is enabled.

Some usernames, such as root, occur on many systems and are therefore not unique across a domain. For those usernames, converting the host portion of the address makes it difficult to sort out where the message really came from and root@owner.foobirds.org and root@foobirds.org is passed through a server that converts both addresses to root@foobirds.org. There is no way for the recipient to know exactly where the message originally originated, and the remote user could not reply to the correct address. The EXPOSED_USER command in Listing 5.3 prevents from masquerading by ensuring that root is not masqueraded.

The primary reason this macro is included in the generic.m4 DOMAIN file is to serve as a warning to the experienced Sendmail administrator that something has changed. Experienced Sendmail administrators may think that root is already part of class E, because prior to Sendmail 8.10 root was the default value for class E. In Sendmail, there are no default values in class E. The EXPOSED_USER(root) command must be added to the configuration if you want to protect root from masquerading. Of course, this command has no real effect in the generic configuration because this configuration does not include any commands to enable masquerading. But the message is clear. If you want to protect the root from masquerading, the EXPOSED_USER command in your configuration.

This command illustrates the main purpose of the generic.m4 file—it is intended as a training tool. The file is designed to show you the type of commands you should include in your own DOMAIN source file. The generic.m4 file is just an example. The DOMAIN source file should be specific to your environment. If you use one, you're expected to create it yourself.

This concludes the DOMAIN file, but it does not conclude the generic-linux.mc macro control file shown in Listing 5.1. There are still two macros in that file to explain. The two source files invoked by the generic-linux.mc macro configuration file are MAILER source files. As the "Eureka! sidebar explains, we know those files didn't cause the problem when we used the generic-linux.cf file, but because they are essential part of every Linux configuration, let's take a look at what they do.

# The Essential Mailers

The two MAILER commands in the generic-linux.mc file are found in most Sendmail configurations. These commands identify the sets of mailers included in the Sendmail configuration.