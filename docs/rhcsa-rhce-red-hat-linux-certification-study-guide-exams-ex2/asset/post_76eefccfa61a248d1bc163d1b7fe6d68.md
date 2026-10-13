
- **statistics** Collects statistics on sendmail usage in binary format. You can read it with the mailstats command. Does not exist until the sendmail service starts processing mail.
- **submit.cf** The main outgoing sendmail configuration file.
- **submit.mc** A macro that you can edit and then generate a new submit.cf file.
- **trusted-users** Lists special users that can send e-mail without warnings.
- **virtusertable** Supports e-mail forwarding; if some users from outside local networks use the local sendmail server, this file supports e-mail forwarding from those domains.

Some of these files require the other sendmail package, sendmail-cf. Use the `rpm -qa | grep sendmail` command to confirm whether these packages are installed. Many of these files are cited in the sendmail.mc file. For example, the following directive incorporates `/etc/mail/virtusertable` in the default sendmail.mc configuration file:

```
FEATURE(`virtusertable',`hash -o /etc/mail/virtusertable.db')dnl
```

You may notice several versions of these files with .db extensions. These are the database files used by sendmail. When you edit files in the /etc/mail directory, the `/etc/mail/make` command, described shortly, processes these files into the .db databases.

There's one more important file, `/etc/aliases`, already described earlier in this chapter. It has the same functionality for both Postfix and sendmail. In other words, it includes a list of forwarders on a local system, from system addresses to the root account, or from one regular user account to another. The `newaliases` command processes this file for sendmail as well.

## The sendmail.mc Macro File

Even the main sendmail macro file, sendmail.mc, can seem intimidating. But very few changes are required to actually get sendmail working. Nevertheless, in case you encounter a slightly different question on an exam, or a somewhat nonstandard question on the job, it's important to understand the contents of the sendmail.mc file.

Macro files for sendmail start with the following divert directive:

```
divert (-1)dnl
```

Each line in the file either starts or ends with the dnl, which is the functional equivalent of the comment character. All information after the dnl is ignored by the sendmail macro preprocessor. If coupled with a divert(0)dnl, all information between the two divert directives is ignored.

The comments that follow provide important directions; the make command in the /etc/mail directory in fact processes all files in the /etc/mail directory:

```
dnl # This is the sendmail macro config file for m4. If you make changes to
dnl # /etc/mail/sendmail.mc, you will need to regenerate the
dnl # /etc/mail/sendmail.cf file by confirming that the sendmail-cf
dnl # package is installed and then performing a
dnl #
dnl #     /etc/mail/make
```

The command that follows includes the noted cf.m4 macro processor, from the sendmail-cf package:

```
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
```

The include directive instructs the make command to read the contents of the named file and insert it at the current location in the output. The quotes in the sendmail.mc file do not conform to standard English usage. This is how additional standard configuration information is left out of the main sendmail.mc macro file.

Incidentally, quoted parameters start with a back quote mark (`) and end with a single quote mark (').

The VERSIONID that follows provides a label for the current configuration:

```
VERSIONID(`setup for linux')dnl
```

The OSTYPE directive that follows specifies the configured operating system:

```
OSTYPE(`linux')dnl
```

The define directive sets files or enables possibly desirable features. Some examples in sendmail.mc support a list of e-mail aliases in the ALIAS_FILE (/etc/aliases), identify where procmail lives (PROCMail_MAILER_PATH), and set basic authentication options (confAUTH_OPTIONS).

One useful option is to avoid advertising the version of sendmail in use, which would otherwise be shown in e-mail message headers. If you activate the following define feature, others don't have to know that you've configured sendmail version 8.14.4.

```
dnl define(`confSMTP_LOGIN_MSG', `$j Sendmail; $b')dnl
```

The commented define directive for a SMART_HOST that follows would be the simplest way to set up forwarding to a smart host, as discussed later in this chapter.

```
dnl define(`SMART_HOST', `smtp.your.provider')dnl
```

Most of the active define options that follow relate to the performance of the sendmail service. The exceptions, shown next, support the use of Procmail for filtering, enable /etc/aliases for substitute e-mail addresses, and require authentication to receive e-mail:

```
define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail')dnl
define(`ALIAS_FILE', `/etc/aliases')dnl
define(`confAUTH_OPTIONS', `A')dnl
```

The problem with the last of these define directives is that it allows plain text authentication. Like the Telnet service, it allows people to send their usernames and passwords over the network in clear text, where anyone who is listening can read that authentication information. Clear text may be appropriate for initial tests and generally conforms to the "basic operation" concept associated with the RHCE objectives. However, for a sendmail service that requires some form of encryption, you could substitute the following directive, which is commented out by default:

```
dnl define(`confAUTH_OPTIONS', `A p')dnl
```

That authentication mechanism, if active, should be coupled with authentication options. The commented directives that follow provide some suggested solutions.

While there's no evidence from the RHCE objectives of an authentication requirement for SMTP services, it is listed in the public Red Hat RH254 course outline, which suggests that you do need to understand the use of Secure Sockets Layer (SSL) certificates, and its successor, Transport Layer Security (TLS). While it's likely unnecessary for SMTP services, it may be helpful to become familiar with some of these authentication mechanisms, as a preview of Chapter 14. To that end, the following commented directives support a variety of authentication mechanisms:

```
dnl TRUST_AUTH_MECH(`EXTERNAL DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
dnl define(`confAUTH_MECHANISMS', `EXTERNAL GSSAPI DIGEST-MD5 CRAM-MD5 LOGIN PLAIN')dnl
```

To support encryption, the following commented section describes the commands required to create a SSL/TLS certificate for sendmail, and its location in the directory tree:

```
dnl # Rudimentary information on creating certificates for sendmail TLS:
dnl # cd /etc/pki/tls/certs; make sendmail.pem
```

```
dnl # Complete usage:
dnl #    make -C /etc/pki/tls/certs usage
dnl #
dnl define(`confCACERT_PATH', `/etc/pki/tls/certs')dnl
dnl define(`confCACERT', `/etc/pki/tls/certs/ca-bundle.crt')dnl
dnl define(`confSERVER_CERT', `/etc/pki/tls/certs/sendmail.pem')dnl
dnl define(`confSERVER_KEY', `/etc/pki/tls/certs/sendmail.pem')dnl
```

The define directive that follows, if activated, would support the use of LDAP authentication:

```
dnl define(`confDONT_BLAME_SENDMAIL', `groupreadablekeyfile')dnl
```

The define directives that follow relate to sendmail behavior for message delays and do not affect basic configuration. The only active directive shown disables timeouts when the server waits for an identification (IDENT) query.

```
dnl define(`confTO_QUEUEWARN', `4h')dnl
dnl define(`confTO_QUEUEBYE', `5d')dnl
dnl define(`confQUEUE_LA', `12')dnl
dnl define(`confREFUSE_LA', `18')dnl
define(`confTO_IDENT', `0')dnl
dnl FEATURE(delay_checks)dnl
```

The FEATURE directives enable specific features. Some administrators configure sendmail to use the submission protocol, in place of SMTP. In that case, you'd want to disable the following directive, which keeps sendmail from listening on port 587:

```
FEATURE(`no_default_msa', `dnl')dnl
```

Other FEATURES relate to specific executable and configuration files. The following specifies the locations of the sendmail shell (smrsh), along with the aforementioned mailertable and virtualusertable databases.

```
FEATURE(`smrsh', `/usr/sbin/smrsh')dnl
FEATURE(`mailertable','hash -o /etc/mail/mailertable.db')dnl
FEATURE(`virtusertable', `hash -o /etc/mail/virtusertable.db')dnl
```

The FEATURE directives that follow support redirection to other e-mail addresses, add the local domain name to an e-mail address if one is not listed, and use files like trusted-users and local-host-names:

```
FEATURE(redirect)dnl
FEATURE(always_add_domain)dnl
FEATURE(use_cw_file)dnl
FEATURE(use_ct_file)dnl
```
