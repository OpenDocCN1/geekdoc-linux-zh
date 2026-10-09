it certainly will confuse some vandals because dccn, or whatever you really use, is nonstandard. Also, remember that many vandals use automated programs to scan Web sites for features and other clues. A nonstandard script alias such as the above is not likely to be incorporated in any automated program.

# ## Use nonextension names for your CGI scripts

Many sites boldly showcase what type of CGI scripts they run. For example:

```
http://www.domain.com/cgi-bin/show-catalog.pl
```

the above URL provides two clues about the site. First, it tells us that the site supports CGI scripts, and second, that the site runs Perl scripts as CGI scripts. If the above site instead used:

```
http://www.domain.com/ext/show-catalog
```

it is harder to determine anything about the site. Use of the `.pl` or `.cgi` extension should be avoided because these extensions provide clues about your system. To change an existing a script's extension from `.pl`, `.cgi`, and so on to a non-extension name, simply rename the script. You do not need to change or add any new Apache configuration for switching to nonextension names.

Like CGI scripts, SSI scripts pose a few security risks. They are discussed below.

# ## Using CGI Scanners

CGI scanners are used to scan a Web server for CGI script-related vulnerabilities. There are two scanners that I like: `cgichk.pl` and Whisker.

# ### cgichk.pl

This is a simple CGI scanner written in Perl. You can download the source from www.packetstorm.securi fy.com. When run from the command line using `perl` `cgichk.pl` command, it asks you to enter a host name for the Web server you want to scan and a port number (default 80). You can also choose to log the results in a file.

`cgichk.pl` first checks the HTTP protocol version being used by the Web server. For example, the following sample session shows that `cgichk.pl` is scanning a host called rhat.nitec.com.

```
CGI scanner [in Perl] v1.1
Host: rhat.nitec.com
HTTP Port [80]:
Log Session?(y/n)
Log File [rhat.nitec.com.scan]:
```