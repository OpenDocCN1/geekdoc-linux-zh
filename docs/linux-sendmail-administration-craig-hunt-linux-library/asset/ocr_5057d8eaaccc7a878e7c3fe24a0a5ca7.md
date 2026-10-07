# Chapter 5 Understanding a Vendor's Configuration

In addition to these two important sets of mailers, there are nine other sets of mailers available with the MAILER command, all of which are covered in Appendix A, "m4 Macro Command Reference." Most of them are very little interest for an average Linux configuration. The two sets of mailers included in the generic-linux.mc configuration are the only ones that most administrators ever use.

# Tweaking the Mailer Configurations

Let's diverge for a moment from the discussion of the generic-linux.mc configuration file to talk about mailer configuration. You're strongly encouraged to create your own DOMAIN source file in the domain directory. You might even be bold to create an OSTYPE file for your Linux distribution in the ostype directory. MAILER source files are different. The mailers loaded by the MAILER macros are defined in the mailer directory. You will never directly edit a file in directory or add any ones files to directory. To modify the settings of a specific mailer, use the configuration variables created for this purpose. Table 5.1 lists the variables used to tune the local and prog mailers and all of the mailers included in the set of SMTP mailers.

# Table 5.1 Mail Configuration Variables

| Variable | Purpose |
|---|---|
| SMTP_MAILER_ARGS | dsmtp mailer arguments. |
| ESMTP_MAILER_ARGS | esmtp mailer arguments. |
| LOCAL_MAILER_ARGS | Arguments for local mail delivery. |
| LOCAL_MAILER_CHAR | Character set for local 8-bit MIME mail. |
| LOCAL_MAILER_DSN_DIAGNOSTIC_CODE | Delivery status notification code used for local mail. |
| LOCAL_MAILER_EOL | End-of-line character for local mail. |
| LOCAL_MAILER_FLAGS | Local mailer flags added to "lsDFMAw5://@q". |
| LOCAL_MAILER_MAX | Maximum size of local mail. |
| LOCAL_MAILER_MAXMSG | Maximum number of messages delivered with a single connection. |