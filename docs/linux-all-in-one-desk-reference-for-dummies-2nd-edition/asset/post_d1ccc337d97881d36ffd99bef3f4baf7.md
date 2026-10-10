
To avoid repeatedly mentioning different file and directory names for different distributions such as Fedora Core and SUSE, I use the file and directory names for Fedora Core in the following discussions. The general discussions apply to **sendmail** in all Linux distributions, but you have to replace the file and directory names with those for your specific distribution.

By defining its own set of high-level macros in files located in the **/usr/share/sendmail-cf** directory, **sendmail** essentially creates its own macro language. The **sendmail** macro files use the **_mc** extension. The primary **sendmail** macro file you configure is **sendmail.mc**, located in the **/etc/mail** directory.

Compared to the **/etc/mail/sendmail.cf** file, the **/etc/mail/sendmail.mc** file is shorter and easier to work with. Here are some lines from the **/etc/mail/sendmail.mc** file that comes with Fedora Core:

```
dnl(1)dnl
dnl # This is the sendmail macro config file for m4. If you make changes to
dnl # /etc/mail/sendmail.mc, you will need to regenerate the
dnl # /etc/mail/sendmail.cf file by confirming that the sendmail-cf package is
dnl # installed and then performing a
dnl #
dnl # make -C /etc/mail
dnl #
include(`/usr/share/sendmail-cf/m4/cf.m4'dnl
VERSIONID(`setup for Red Hat Linux')dnl
OSTYPE(`linux')dnl
dnl #
dnl # default logging level is 9, you might want to set it higher to
dnl # debug the configuration
dnl define(`confLOG_LEVEL', `9')dnl
dnl #
dnl # Uncomment and edit the following line if your outgoing mail needs to
dnl # be sent out through an external mail server:
dnl #
dnl define(`SMART_HOST', smtp.comcast.net')
....lines deleted ...
dnl #
dnl MASQUERADE_AS('mydomain.com')dnl
dnl #
dnl # masquerade not just the headers, but the envelope as well
dnl FEATURE(masquerade_envelope)dnl
dnl #
dnl # masquerade not just @mydomainalias.com, but @*.mydomainalias.com as well
dnl #
dnl FEATURE(masquerade_entire_domain)dnl
dnl MASQUERADE_DOMAIN(localhost.localdomain)dnl
dnl MASQUERADE_DOMAIN(mydomainalias.com)dnl
dnl MASQUERADE_DOMAIN(mydomain.lan)dnl
MAILER(smtp)dnl
MAILER(procmail)dnl
dnl MAILER(cyrusv2)dnl
```

If you make changes to the /etc/mail/sendmail.mc file, you must generate the /etc/mail/sendmail.cf file by running the sendmail.mc file through the m4 macro processor with the following command. (You have to log in as **root**.)

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

The comments also tell you that you need the **sendmail-cf** package to process this file.

From the previous section's description of m4 macros, you can see that the **sendmail.mc** file uses **define** to create new macros. You can also see the liberal use of dnl to avoid inserting too many blank lines into the output.

The other uppercase words (such as **OSTYPE**, **FEATURE**, and **MAILER**) are sendmail macros. These are defined in the .m4 files located in the subdirectories of the /usr/share/sendmail-cf directory and are incorporated into the sendmail.mc file with the following *include* macro:

```
include(`/usr/share/sendmail-cf/m4/cf.m4') dnl
```

The /usr/share/sendmail-cf/m4/cf.m4 file, in turn, includes the cfdhead.m4 file, which includes other m4 files, and so on. The net effect is that, as the m4 macro processor processes the sendmail.mc file, the macro processor incorporates many m4 files from various subdirectories of /usr/share/sendmail-cf.

Here are some key points to note about the /etc/mail/sendmail.mc file:

- **VERSIONID**(`setup for Red Hat Linux') macro inserts the version information enclosed in quotes into the output.
- **OSTYPE**(`linux') specifies Linux as the operating system. You have to specify this macro early to ensure proper configuration. Placing this macro right after the **VERSIONID** macro is customary.
- **MAILER**(smtp) describes the mailer. According to instructions in the /usr/share/sendmail-cf/README file, **MAILER** declarations are always placed at the end of the sendmail.mc file, and **MAILER**(smtp) always precedes **MAILER**(procmail). The mailer **smtp** refers to the SMTP mailer.
- **FEATURE** macros request various special features. For example, FEATURE(`blacklist_recipients') turns on the capability to block incoming mail for certain usernames, hosts, or addresses. The specification for what mail to allow or refuse is placed in the access database (stored in /etc/mail/access.db file). You also need the FEATURE(`access_db') macro to turn on the access database.
- **MASQUERADE_AS**(`mydomain.com') causes sendmail to label outgoing mail as having come from the host mydomain.com (replace with your domain name). The idea is for a large organization to set up a single sendmail server that handles the mail for many subdomains and makes everything appear to come from a single domain. (For example, mail from many departments in a university appears to come from the university’s main domain name.)
- **MASQUERADE_DOMAIN**(subdomain.mydomain.com) instructs sendmail to send mail from an address such as user@subdomain.mydomain.com as having originated from the same username on the domain specified by the MASQUERADE_AS macro.

The sendmail macros such as FEATURE and MAILER are described in the /usr/share/sendmail-cf/README file. Consult that file to find out more about the sendmail macros before you make changes to the sendmail.mc file.

## sendmail.cf file syntax

The sendmail.cf file's syntax is designed to be easy to parse by the sendmail program because sendmail reads this file whenever it starts. Human readability was not a primary consideration when the file's syntax was designed. Still, with a little explanation, you can understand the meaning of the control lines in sendmail.cf.

Each sendmail control line begins with a single-letter operator that defines the meaning of the rest of the line. A line that begins with a space or a tab is considered a continuation of the previous line. Blank lines and lines beginning with a pound sign (#) are comments.

Often, no space is between the single-letter operator and the arguments that follow the operator, which makes the lines even harder to understand. For example, sendmail.cf uses the concept of a class—essentially a collection of phrases. You can define a class named P and add the phrase REDIRECT to that class with the following control line:

```
CPREDIRECT
```

Because everything is jumbled together, the command is hard to decipher. On the other hand, to define a class named `Accept` and set it to the values `OK` and `RELAY`, write the following:

```
C{Accept}OK RELAY
```

This command may be slightly easier to understand because the delimiters (such as the class name, `Accept`) are enclosed in curly braces.

Other—more recent—control lines are even easier to understand. For example, the line `O HelpFile=/etc/mail/helpfile` defines the option `HelpFile` as the filename `/etc/mail/helpfile`. That file contains help information sendmail uses when it receives a `HELP` command.

Table 4-1 summarizes the one-letter control operators used in sendmail.cf. Each entry also shows an example of that operator. This table helps you understand some of the lines in sendmail.cf.

### Table 4-1 Control Operators Used in sendmail.cf

| Operator | Description |
| :--- | :--- |
| C | Defines a class; a variable (think of it as a set) that can contain several values. For example, `Cwlocalhost` adds the name `localhost` to the class `w`. |
| D | Defines a macro, a name associated with a single value. For example, `DnMAILER-DAEMON` defines the macro `n` as `MAILER-DAEMON`. |
| F | Defines a class that's been read from a file. For example, `Fw/etc/mail/local-host-names` reads the names of hosts from the file `/etc/mail/local-host-names` and adds them to the class `w`. |
| H | Defines the format of header lines that sendmail inserts into a message. For example, `H??From: < $g >` defines the `Return-Path` field of the header. |
| K | Defines a map (a key-value pair database). For example, `Karighth` defines the map named `arith` as the compiled-in map of the same name. |
| M | Specifies a mailer. The following lines define the `procmail` mailer: `Mprocmail, Pa=/usr/bin/procmail, F=DIFGMSPhmu9, S=EnvFromSMTP/HdrFromSMTP, R=EnvToSMTP/HdrFromSMTP, T=DNS/RFC822/X-Unix, A=procmail -Y -m $h $f $u`. |
