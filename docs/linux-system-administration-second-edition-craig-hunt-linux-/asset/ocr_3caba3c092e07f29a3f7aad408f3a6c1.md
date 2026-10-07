suse-security-announce. Other lists are specific to Motif, Oracle, IMAP, Applixware, and other topics. More information on these lists is available at http://www.suse.com/support/us/mailinglists/index.html.

A number of sites archive the various Linux-related lists. Very useful is Google.com's site, located at http://www.google.com/. What you'll find there is a search engine that will perform various Web searches to include a groups search that will respond to your query with a list of related posts from the various lists that are archived there. Select the one that most closely resembles what you're interested in, and you'll see the text from that post. It's especially useful to enter error messages as the query, possibly followed by the word Linux. This works quite well for those errors that don't seem to be documented anywhere else.

For example, you might enter the following in the search window:

```
"You don't exist; go away" Linux
```

This generates about 1720 hits; several of these detail the problem. (In case you're curious, the error means there is no utmp entry for your shell or you don't own the tty/pty you're logged in on.)

# ## Webmin

There are several administrative tools available. Many distributions create their own custom tools. To avoid having to use a different tool on computers using different distributions, we recommend the use of the Webmin tool for administrative tasks. Webmin performs most of the major system administration tasks that you'll need. Webmin is used via a Web browser like Netscape. If you use version 7.2 or newer, Webmin is Secure Socket Layer (SSL) enabled by default, so you will have to use the secure version of the HTTP: HTTPS.

To install Webmin, download the latest rpm and move it to /usr/local/packages or wherever you choose to store packages that you download and install.

Change the directory to /usr/local/packages and use the appropriate rpm command to install. For example, webmin-0.92-1.i386.rpm would be installed using the following command:

```
# rpm -uhv webmin-0.92-1.i386.rpm
```

**Note** Remember that if you use the u for update and the package doesn't already exist, it will be installed. If it does already exist, it will be updated instead.

To test the installation, bring up your browser to port 10000 using SSL on the localhost. With Netscape, the command would look like this:

```
netscape http://localhost 10000
```

Next log in as root with your regular root password.

# ## Command-Line Tools

Linux provides a number of command-line tools to support you in your system administration duties. This section first looks at the command-line techniques that help you use commands more effectively, like pipes, redirection, wildcards, and tildes. As you'll see, all of these features are