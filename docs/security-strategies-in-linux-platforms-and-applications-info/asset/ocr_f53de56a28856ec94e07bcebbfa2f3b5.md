# PART 2 Layered Security and Linux

But that's also a weakness, since the nmap command can detect the services running on obscure ports.

# Obscurity by Other Means

The use of nonstandard open ports is just one way to obscure local systems and networks. Services can be obscured by their login messages. Services can also be obscured by their error messages. While Chapter 8 covers the Secure Shell (SSH), the following directive in the main configuration file (/etc/ssh/sshd_config) points to the /etc/issue.net file as the login message for users:

Banner /etc/issue.net

Once configured, you can add appropriate legal warnings or other messages that may mislead a black-hat hacker. The file is associated with login messages to Telnet, which you choose to take the risks associated with that protocol, which transmits sensitive information in clear text. For that reason and others, the use of Telnet is not recommended.)

As for errors, the information shown when a user navigates to a non-existent Web page can also be important. If you're using the Apache Web server, that information depends on the ServerTokens directive in the associated configuration file. Full information leads to the following message when a user tries to navigate to a nonexistent Web page:

+   - Apache/2.0.63 (Unix) OpenSSL/0.9.8e/0.9.8e-fips-rhel5
- JRUN/4.0 mod_auth_paththrough/2.1 mod_bwlwimited/1.4
- FrontPage/5.0.2.2635 Server at example.com Port 80

That's a lot of information a black-hat hacker may be able to use. Assuming the noted Web server actually includes the noted versions of the listed software, black-hat hacker should be able to check for known flaws in each of those systems.

If Apache were configured with a less informative setting, the user would see the following information instead:

Apache Server at example.com Port 80

That's a lot less information for a black-hat hacker. In other words, obscurity can make it more difficult for a black-hat hacker to break into your systems.

# Protect with TCP Wrappers

The TCP Wrappers system was originally developed to protect the services controlled through the internet server and extended internet server services described in Chapter 6. It's extended statically and dynamically to additional services as will be described shortly. You'll see how such services can be protected through /etc/hosts.allow and /etc/hosts.deny configuration files.