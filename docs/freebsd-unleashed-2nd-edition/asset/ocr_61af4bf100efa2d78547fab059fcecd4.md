buggy CGI scripts, and hackers abound. It’s a fairly simple matter for a user to create a CGI program owned by root, put it in his directory, and wait for it to be executed as the owner (the super-user), unleashing its destructive payload against any files in your system.

CGIWrap protects your system against such problems. It’s not a complete or ideal solution, but it reduces the security risks associated with user CGI scripts so that you can put your administrative efforts elsewhere. By running security checks against all user CGI programs before executing them, and by running each program as its owner, CGIWrap shifts the risks inherent in a badly written CGI from you onto the script’s owner.

When you install CGIWrap from its port directory, the cgiwrap program (a precompiled binary) goes into your top-level cgi-bin directory, /usr/local/www/cgi-bin. Rather than operating as a wrapper around Apache itself as suexec does, CGIWrap has to be called explicitly by your users, with a URL of the following form:

http://www.somewhere.com/cgi-bin/cgiwrap/frank/myscript.cgi

Or as a server-side include:

```
<!--#include virtual="/cgi-bin/cgiwrap/frank/myscript.cgi"-->
```

This executes the myscript.cgi program in /home/frank/public_html/cgi-bin. All of a user’s CGI programs must go inside his or her public_html/cgi-bin directory, which the user needs to create if it doesn’t exist already.

> **TIP**
> 
> CGI programs outside the public_html/cgi-bin directory will not be run through CGIWrap, so it’s important that you disable CGI execution outside the server DocumentRoot. To do so, make sure you don’t have an Options +ExecCGI directive in a block that defines your users’ directories.

The official CGIWrap home page is at http://cgiwrap.unixtools.org/, for further reference.

> **Preventing SMTP Relaying**
> 
> It can be construed as a security weakness for your Sendmail server to be open for anybody to send mail through it. These days, an open mail relay is almost synonymous with a mail server that’s being used by spammers to broadcast junk mail, and that constitutes a theft of your services. Furthermore, you’re subject to a form of denial of service if other mail service providers add your host to a “blackhole” list—a list of banned remote addresses with which they refuse to exchange any mail—as a result of your server being an open and unprotected mail relay.
> 
> It is critical to configure Sendmail so that your own legitimate users and their correspondents can continue to use your SMTP server, but unauthorized spammers—who want to send mail that neither originates on nor is destined for your server—cannot. You can find a full description of how this can be achieved in the “Notes on Relaying” section of Chapter 24.