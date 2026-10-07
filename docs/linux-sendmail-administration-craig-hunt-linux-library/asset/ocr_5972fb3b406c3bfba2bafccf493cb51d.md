DOMAIN The DOMAIN macro loads a file that contains information specific to your domain or network. The DOMAIN source file is a perfect place for commands that affect hostnames and domain names, and define values, such as mail relay names, because the information is specific to your domain, you must create your own DOMAIN source file. The Sendmail code distribution provides a sample DOMAIN source file, named generic.m4, that you can use as a starting point for creating your own configuration. As you created a DOMAIN source file that called foobirds.m4. The following command, placed in the macro control file, uses foobirds.m4 to help in building the sendmail.cf:

DOMAIN(foobirds)

The DOMAIN command is optional. When it is used, it normally appears only in the macro configuration file.

MAILER The MAILERS identify the various sets of macro definitions that should be included in the sendmail.cf. A usable configuration must have at least one MAILER command; almost every Linux configuration has the following two:

MAILER(local) The MAILER(local) macro command adds the local mailer and the prog mailer to the configuration. The local and prog mailers are essential, so any usable configuration will have at least this MAILER command.

MAILER(smtp) The MAILER(smtp) macro adds mailers for SMTP, Extended SMTP, eight-bit SMTP, directed SMTP, and relayed mail. Every Linux system that sends SMTP mail, whether directly or through a mail server, has this MAILER command.

In addition to these two important sets of mailers, there are nine other sets of mailers available with the MAILER command. Most of them are very little interest to the average system administrator, but for the sake of completeness they are all covered in Appendix A, "m4 Macro Command Reference."

OSTYPE, DOMAIN, and MAILER are generally found only in the macro configuration file. The other four commands are found in Table 4.1 in both macro configuration and macro source files:

VERSIONID The VERSIONID macro defines version control information. This macro is optional, but is found in m4 files. The command has no required format for the argument. Use any version control information you desire. The basic format of the VERSIONID macro is:

```
VERSIONID(`version-control-data`)
```

![](bbox=[0.933, 0.2735, 0.992, 0.3735])