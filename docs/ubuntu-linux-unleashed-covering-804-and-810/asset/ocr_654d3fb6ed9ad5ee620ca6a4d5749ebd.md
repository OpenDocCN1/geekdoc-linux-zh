# Configuring Fetchmail

After you have installed Fetchmail, you must create the file .fetchmailrc in your home directory, which provides the configuration for the Fetchmail program.

You can create and subsequently edit the .fetchmailrc file by using any text editor. The configuration file is straightforward and quite easy to create; the following sections explain the manual method for creating and editing the file. The information presented in the following sections does not discuss all the options available in the .fetchmailrc file, but covers the most common ones needed to get a basic Fetchmail installation up and running. You must use a text editor to create the file to include entries like the ones shown as examples—modified for your personal information, of course. For advanced configuration, see the man page for Fetchmail. The man page is well written and documents all the configuration options in detail.

# CAUTION

The .fetchmailrc file is divided into three different sections: global options, mail server options, and user options. It is important that these sections appear in the order listed. Do not add options to the wrong section. Putting options in the wrong place is one of the most common problems that new users make with Fetchmail configuration files.

# Configuring Global Options

The first section of .fetchmailrc contains the global options. These options affect all the mail servers and user accounts that you list later in the configuration file. Some of these global options can be overridden with local configuration options, as you learn later in this section. Here is an example of the options that might appear in the global section of the .fetchmailrc file:

```
set daemon 600
set postmaster foobar
set logfile ./fetchmail.log
```

The first line in this example tells Fetchmail that it should start in daemon mode and check the mail servers for new mail every 600 seconds, or 10 minutes. Daemon mode means that after Fetchmail starts, it will move itself into the background and continue running. Without this line, Fetchmail would check for mail once when it started and would then terminate and never check again.

The second option tells Fetchmail to use the local account foobar as a last-resort address. In other words, any email that it receives and cannot deliver to a specified account should be sent to foobar.