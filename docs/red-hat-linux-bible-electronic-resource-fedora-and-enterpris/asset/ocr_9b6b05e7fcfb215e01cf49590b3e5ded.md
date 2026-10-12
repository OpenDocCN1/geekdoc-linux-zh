simplify the creation of the sendmail.cf file. So, the steps I recommend for configuring sendmail are as follows:

+   Edit the /etc/sendmail.mc file. Most of what you need to do to configure sendmail can be done by editing this file.

+   Generate the sendmail.cf file from the edited sendmail.mc file. This is done using the m4 processor.

+   Review your sendmail.cf configuration. If you want to make changes, modify the sendmail.mc file and regenerate sendmail.cf.

> NOTE: The m4 macros you use in the sendmail.mc file are different from the resulting settings in the sendmail.cf file. To find out what macros to use for a setting you find in the sendmail.cf file, refer to the /usr/share/doc/sendmail/README.cf file.

+   Restart the sendmail server.

> WARNING: Because of the way sendmail in configured in Red Hat Linux, you should not directly modify the sendmail.cf file. The sendmail.cf file is automatically regenerated when sendmail restarts if sendmail.mc changes. As a result, any modifications made directly to sendmail.cf will be lost.

The following sections provide details for this process.

# Configuring the sendmail.mc file

The following code samples are from the /etc/mail/sendmail.mc file that accompanies Red Hat's version of sendmail.

> NOTE: Lines that begin with dnl (delete to new line) followed by comment characters (###) in the sendmail.mc file are comment lines. In most cases, I have left them out in the examples shown.

```
divert(-1)dnl
include(\`/usr/share/sendmail-cf/m4/cf.m4\`\'dnl
VERSIONID(\`setup for Red Hat Linux\`\'dnl
OSTYPE(\`linux\`\'dnl
```

The first few lines of the sendmail.mc file do some housekeeping. The divert line removes extra output when the configuration file is generated. The include line causes rule sets needed by sendmail to be included. The VERSIONID line identifies the configuration file as being for Red Hat (though this setting is not checked, so it could be anything you like). The OSTYPE, however, must be set to linux to get the proper location of files needed by sendmail.

```
dnl\ define(\`SMART_HOST\',\`smtp.your.provider\`)
```

By default, the sendmail daemon tries to send your outgoing e-mails directly to the mail server to which they are addressed. If you want all e-mail to be relayed through a particular mail