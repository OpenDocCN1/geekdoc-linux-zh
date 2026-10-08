at least a little protection from attack. However, be aware that if your users are online, anyone in the world can start sending messages to them. This should send a shiver down your back. With e-mail, at least, either you are using a virus filter or you have disabled mail clients from loading attachments automatically.

# A.6 Web Server Policy

> DANGER LEVEL ☠️☠️☠️☠️☠️

Web server policy should address both security and legal issues. The security issues addressed should be designed to protect the server from attack (and to have a plan of action if it is attacked).

Frequently, a literary or artistic type of person will be designing the content of Web pages but might not have the security knowledge that you do. The strictest policy would be to have all installs and changes done by the SysAdmin or, possibly, by a Webmistress who is highly experienced to dominate the security problems.

This might be too strict. Perhaps you should have those who install nonactive Web pages and images be required to use an account that has an umask of 022. It would be different from the account that may add or alter CGI scripts and programs, the Web server (Apache) configuration files, and other more security-sensitive files. Under no circumstances should non-SysAdmins (other than knowledgeable Webmasters) be allowed to add or change CGI scripts and programs, configuration files, etc.

All CGI programs and scripts, Apache modules, etc., should come only from trusted sources and still should be carefully scanned and even tested to verify no security bugs. Consider something as simple as a CGI program that is called from an HTML form to accept text comments from a browser. It might fork off Mail to send data to a dedicated e-mail address, but easily could have bugs that allow even a novice cracker to make herself root, merely by throwing a semicolon in the Subject text, followed by any root command she desires and another semicolon.

If the CGI script is not extremely careful, it might be doing something like the following. In this C example, the program is building a shell command from the subject that the browser has supplied, presumably to generate e-mail to the Webmistress.

```
char           *subject;
char           buf[200];
FILE           *fp;

sprintf(buf, "Mail -s '%s' webmistress@turkey.com", subject);
fp = fopen(buf, "w");
```

The grave security hole is that the user's input is not checked for validity. If the user supplies a subject of