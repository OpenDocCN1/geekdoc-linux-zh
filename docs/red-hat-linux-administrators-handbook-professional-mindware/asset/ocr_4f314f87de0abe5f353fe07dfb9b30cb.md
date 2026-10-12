Before running the CGI or SSI command, the suEXEC wrapper performs a set of tests to ensure that the request is valid. Among other things, this testing procedure ensures that the CGI script is owned by a user who is allowed to run the wrapper and that the CGI directory or the CGI script is not writable by anyone but the owner. After the security checks are successful, the suEXEC wrapper changes the UID and the GID to the target UID and GID via setuid and setgid calls, respectively. The group-access list is also initialized with all groups in which the user is a member, suEXEC cleans the process's environment by establishing a safe execution PATH (defined during configuration), as well as by passing through only those variables whose names are listed in the safe environment list (also created during configuration). The suEXEC process then becomes the target CGI application or SSI command and executes. This may seem like a lot of work—and it is—but this provides a greater security coefficient, as well.

If you are interested in installing suEXEC support in Apache, run the configure (or config\_status) script as follows:

```
. /configure --prefix=/path/to/apache \
--enable-suexec \
--suexec-caller=httpd \
--suexec-userdir=public\_html
--suexec-uidmin=100 \
--suexec-gidmin=100
--suexec-
safepath="/usr/local/bin:/usr/bin:/bin"
```

Here is the detailed explanation of this configuration:

+   **--enable-suexec.** Enables suEXEC support.

+   **--suexec-caller=httpd.** Change *httpd* to the UID you use for the User directive in the Apache configuration file. This is the only user who will be permitted to run the suEXEC program.

+   **--suexec-userdir=public\_html.** Defines the subdirectory under users' home directories where suEXEC executables are to be kept. Change *public\_html* to whatever you use as the value for the UserDir directive, which specifies the document root directory for a user's Web site.