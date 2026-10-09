```
Searching for edit.pl : Not Found
Searching for perlshop.cgi : Not Found
Searching for anyboard.cgi : Not Found
Searching for webbbs.cgi : Found!
Searching for environ.cgi : Not Found
Searching for whois_raw.cgi : Not Found
Searching for _vti_inf.html : Not Found
Searching for service.pwd : Not Found
Searching for users.pwd : Not Found
Searching for authors.pwd : Not Found
Searching for administrators : Not Found
Searching for shtml.dll : Not Found
Searching for shtml.exe : Not Found
Searching for args.bat : Not Found
Searching for uploader.exe : Not Found
Searching for rguest.exe : Not Found
Searching for wguest.exe : Not Found
Searching for bd1r - samples : Not Found
Searching for CGImail.exe : Not Found
Searching for newsn.exe : Not Found
Searching for fpcount.exe : Not Found
Searching for counter.exe : Not Found
Searching for visadmin.exe : Not Found
Searching for openfile.cfm : Not Found
Searching for expcalc.cfm : Not Found
Searching for disposedfile : Not Found
Searching for sendmail.cfm : Not Found
Searching for codebrws.asp : Not Found
Searching for codebrws.asp 2 : Not Found
Searching for showcode.asp : Not Found
Searching for search97.vts : Not Found
Searching for carco.dll : Not Found
Server may have CGI vulnerabilities.
```

Notice the line in bold. The scan found a potential CGI security risk. The webbbs.cgi script can be abused by script kiddies and wanna-be hackers to break into the system. If your scan identifies one or more security risks, consider removing the scripts or updating them with appropriate fixes.

# Whisker

Whisker is a Perl-based CGI scanner that I like a lot. You can download the source distribution from www.filesearch.ru. After it is downloaded, extract the source in a directory and run the whisker.pl script as perl whisker.pl -h hostname. For example, perl whisker -rh at.nitec.com command runs the scanner on the Apache Web server running on the named host. The result is shown below:

```
Host: rhat.nitec.com
= Server : Apache/2.0.14 (Unix)
+ 200 OK: HEAD /cgi-bin/webbbs.cgi
+ 200 OK: HEAD /manual/
+ 200 OK: HEAD /temp/
```