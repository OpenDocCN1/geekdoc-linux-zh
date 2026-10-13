
Be more careful, because the possible damage will affect his or her content solely. In one shot, you get increased user responsibility and awareness and, simultaneously, a limited area for potential damage. To run a CGI application using a UID other than the Apache server, you need a special type of program called a wrapper, which enables you to run a CGI application as the user who owns the file rather than as the Apache server user. Some CGI wrappers do other security checks before they run the requested CGI applications. The following sections cover two popular CGI wrappers.

## suEXEC

Apache comes with a support application called suEXEC that provides Apache users with the ability to run CGI and SSI programs under UIDs that are different from the UID of Apache. suEXEC is a setuid wrapper program that is called when an HTTP request is made for a CGI or SSI program that the administrator designates to run as a UID other than that of the Apache server. When such a request is made, Apache provides the suEXEC wrapper with the program's name and the UID and GID. suEXEC runs the program using the given UID and GID.

Before running the CGI or SSI command, the suEXEC wrapper performs a set of tests to ensure that the request is valid. Among other things, this testing procedure ensures that the CGI script is owned by a user who is allowed to run the wrapper and that the CGI directory or the CGI script is not writable by anyone but the owner. After the security checks are successful, the suEXEC wrapper changes the UID and the GID to the target UID and GID via setuid and setgid calls, respectively. The group-access list is also initialized with all groups in which the user is a member. suEXEC cleans the process's environment by establishing a safe execution PATH (defined during configuration), as well as by passing through only those variables whose names are listed in the safe environment list (also created during configuration). The suEXEC process then becomes the target CGI application or SSI command and executes. This may seem like a lot of work — and it is — but this provides a greater security coefficient, as well.

### Configuring and installing suEXEC

If you are interested in installing suEXEC support in Apache, run the configure (or config.status) script as follows:

```
./configure --prefix=/path/to/apache \
    --enable-suexec \
    --suexec-caller=httpd \
    --suexec-userdir=public_html \
    --suexec-uidmin=100 \
    --suexec-gidmin=100 \
    --suexec-safepath="/usr/local/bin:/usr/bin:/bin"
```

Here is the detailed explanation of this configuration:

- **--enable-suexec.** Enables suEXEC support.
- **--suexec-caller=httpd.** Change httpd to the UID you use for the User directive in the Apache configuration file. This is the only user who will be permitted to run the suEXEC program.
- **--suexec-userdir=public_html.** Defines the subdirectory under users' home directories where suEXEC executables are to be kept. Change public_html to whatever you use as the value for the UserDir directive, which specifies the document root directory for a user's Web site.
- **--suexec-uidmin=100.** Defines the lowest UID permitted to run suEXEC-based CGI scripts. In other words, UIDs below this number won't be able to run CGI or SSI commands via suEXEC. Look at your /etc/passwd file to make sure the range you chose does not include the system accounts that are usually lower than UIDs below 100.
- **--suexec-gidmin=100.** Defines the lowest GID permitted to be a target group. In other words, GIDs below this number won't be able to run CGI or SSI commands via suEXEC. Look at your /etc/group file to make sure the range you chose does not include the system account groups that are usually lower than UIDs below 100.
- **--suexec-safepath="/usr/local/bin:/usr/bin:/bin".** Defines the PATH environment variable that gets executed by suEXEC for CGI applications and SSI commands.

### Enabling and testing suEXEC

After you install both the suEXEC wrapper and the new Apache executable in the proper location, restart Apache, which will write a message similar to this:

[notice] suEXEC mechanism enabled (wrapper:
/usr/local/sbin/suexec)

This tells you that the suEXEC is active. Now, test suEXEC's functionality. In the srm.conf file, add the following lines:

```
UserDir public_html
AddHandler cgi-script .pl
```

The first directive (UserDir) sets the document root of a user's Web site to be ~username/public_html, where username can be any user on the system. The second directive associates the cgi-script handler with the .pl files. This is done to run Perl scripts with .pl extensions as CGI scripts. For this test, you will need a user account. In this example, I will use the host wormhole.nitec.com and a user called kabir. Copy the script shown in Listing 12-2 to a file and put it in your user's public_html directory. In my case I put the file in the ~kabir/public_html directory.

### Listing 12-2 A CGI Script to Test suEXEC Support

```perl
#!/usr/bin/perl
#
# Make sure the preceding line is pointing to the
# right location. Some people keep perl in
# /usr/local/bin.

my ($key,$value);
print "Content-type: text/html\n\n";
print "<h1>Test of suEXEC</h1>";

foreach $key (sort keys %ENV){
$value = $ENV{$key};
print "$key = $value <br>";
}
exit 0;
```

To access the script via a Web browser, I request the following URL:

```
http://wormhole.nitec.com/~kabir/test.pl
```

A CGI script is executed only after it passes all the security checks performed by suEXEC. suEXEC also logs the script request in its log file.

The log entry for my request looks as follows:

```
[1998-12-23 16:00:22]: uid: (kabir/kabir) gid:
(kabir/kabir) cmd: test.pl
```

If you are really interested in knowing that the script is running under the user's UID, insert a sleep command (such as sleep(10);) inside the foreach loop, which will slow down the execution and allow you to run commands such as top or ps on your Web server console to find out the UID of the process running test.pl. You also can change the ownership of the script using the chown command, try to access the script via your Web browser, and see the error message that suEXEC logs. For example, when I change the ownership of the test.pl script in the ~kabir/public_html directory as follows:

```
chown root test.pl
```

I get a server error, and the log file shows the following line:

```
[1998-12-23 16:00:22]: uid/gid (500/500) mismatch with directory (500/500) or program (0/500)
```

Here, the program is owned by UID 0, and the group is still kabir (500), so suEXEC refuses to run it, which means suEXEC is doing what it is supposed to do.

Further, if these directives are specified for a <VirtualHost> container, the server user ID or group ID is assumed.

For security and efficiency reasons, all suEXEC requests must remain within either a top-level document root for virtual host requests or one top-level personal document root for userdir requests. For example, if you have four virtual hosts configured, you need to structure all of your virtual host document roots off of one main Apache document hierarchy to take advantage of suEXEC for virtual hosts.

## CGIWrap

CGIWrap is like the suEXEC program insofar as it permits users to use CGI applications without compromising the security of the Web server. CGI programs are run with the file owner's permission. In addition, CGIWrap performs several security checks on the CGI application and will not be executed if any checks fail.

CGIWrap is written by Nathan Neulinger; the latest version of CGIWrap is available from the primary FTP site on ftp://ftp.cc.umr.edu/pub/cgi/cgiwrap/. CGIWrap is used via a URL in an HTML document. As distributed, CGIWrap is configured to run user scripts that are located in the ~/public_html/cgi-bin/ directory.

### Configuring and installing CGIWrap

CGIWrap is distributed as a gzip-compressed tar file. You can uncompress it by using gzip and extract it by using the tar utility.

Run the Configure script, which prompts you to answer many questions. Most of these questions are self-explanatory. Also note that there is a feature in this wrapper that differs from suEXEC. It enables you to create allow and deny files that can be used to restrict access to your CGI applications. Both of these files have the same format, as shown in the following:

```
User ID
mailto:Username@subnet1/mask1,subnet2/mask2. . .
```

You can either have a single username (nonnumeric UID) or a user mailto:ID@subnet/mask line where one or more subnet/mask pairs can be defined. For example, if the following line is found in the allow file (you specify the filename),
