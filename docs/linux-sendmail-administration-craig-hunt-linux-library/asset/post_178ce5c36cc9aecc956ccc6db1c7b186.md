
the test.mc file can be processed with the following m4 command:

```
[root]# m4 test.mc > test.cf
```

Readers who use commands in other languages generally think the include command can be used to separate a complex configuration into several files and then bring those files together for processing. While that is true for m4, it is not true for Sendmail configuration. All macro configuration files are short files that do not benefit from being segmented. The only time you'll see include used in the files provided with the Sendmail distribution is when cf.m4 itself includes the large and complex cfhead.m4 file. The only time you will use include is when you want to include the cf.m4 file into your macro configuration file to simplify the m4 command.

The LOCAL_CONFIG, LOCAL_RULESET, and LOCAL_RULE_n commands allow you to put raw sendmail.cf configuration directly in the m4 source file. These commands, and related commands, mean everything that can be done in the m4 macro source files. (sendmail.cf configuration commands are discussed in Chapter 7.) We use the LOCAL_CONFIG, LOCAL_RULESET, and LOCAL_RULE_n commands several times in the text to define complex sendmail.cf configurations.

The MODIFIER_MAILER_FLAGS command is used to override the flags for a mailer. Mailer flags are found in Chapter 7, "Sendmail File," and a listing of all the names of mailer flags is found in Appendix C, "Sendmail Variables, Options, and Flags." The MODIFIER_MAILER_FLAGS command has two arguments: the name of the mailer and the flag to be modified. A flag is preceded by a a + if it is to be added to the existing set of flags or a - if an existing flag is to be removed.

The MASQUADE_AS and EXPOSED_USER commands deal with masquerading. Frequently, an organization allows all of its outbound mail to appear as if it came from one source to create clean and consistent e-mail addresses, and to hide the names of internal systems that should not be receiving mail. Masquerading is the name for this type of mail rewriting. MASQUADE_AS defines the hostname that is used as the hostname for all outbound mail. If MASQUADE_AS('foobirds.org') is set in the configuration, from craig@w.foobirds.org goes out as craig@foobirds.org.

EXPOSED_USER addresses a problem created by masquerading. Assume that mail from root@w.foobirds.org and root@ibis.foobirds.org is passed through the server with the MASQUADE_AS('foobirds.org') setting. If both addresses are rewritten to root@foobirds.org, you have a problem. There is no way for the recipient to know exactly where the message originated, and the remote user could not reply to the correct address. Usernames, like root, are found on every system not masqueraded. The EXPOSED_USER command is used to define the usernames that should not be masqueraded.

Masquerading is covered extensively in Chapter 9, "Special m4 Configurations." There are several more m4 commands that relate to masquerading, all of which will be covered in that chapter.

The commands in Table 4.1 and Table 4.3 are just the tip of the m4 iceberg. Many more commands are covered in Part 2 of the text as examples of advanced configurations, and all of the m4 commands are covered in Appendix A. This chapter does not provide exhaustive cover of the m4 language. it is an introduction to m4 that helps you understand the m4 commands contained in the sample files. Understanding these basic commands should help you read the macro configuration file provided by your vendor, which is a topic we tackle in Chapter 5, "Understanding a Vendor's Configuration."

# In Sum

Sendmail reads its configuration from the sendmail.cf file. However, this file is not directly configured by the Sendmail administrator. Instead the file is constructed inductively from m4 macros.

The Sendmail distribution provides the m4 source files necessary to build a Sendmail configuration. The m4 source files are contained in the nine subdirectories of the cf directory. for most configurations, each of the nine subdirectories can be ignored because they are either unused nor they contain source files that are never modified by the system administrator. The only subdirectory that the administrator needs to work with for most config is the cf/cf directory.

The cf/cf directory contains the macro configuration files. The Sendmail administrator creates a macro configuration file that selects the source files that provide the features necessary for the Sendmail configuration. Most macro configuration files are not built from scratch. The Sendmail distribution provides about 20 different sample macro configuration files. You select a macro configuration file that matches your needs and only make small adjustments if they are necessary.

The macro configuration file is then processed through m4 to produce the sendmail.cf file. But even this step may not be necessary if you do not change the sample macro configuration file for your configuration. Several Sendmail configuration files built from sample configuration files are included in the cf/cf directory.

To select and modify the correct m4 macro configuration file, you must have a base understanding of the m4 macro configuration language. Use the tables in this chapter and the list of configuration commands in Appendix A to help you read and modify the macro configuration file.

![](img/9639113aa446fb8976cb3d377f7aafdd_128_0.png)

macro configuration file. Use the tables in this chapter and the list of configuration commands in Appendix A to help you read and modify the macro configuration file.

![](img/9639113aa446fb8976cb3d377f7aafdd_128_0.png)

# Understanding a Vendor’s Configuration

Sendmail reads its configuration from the sendmail.cf file. However, this file is not directly configured by the Sendmail administrator. Instead the file is constructed inductively from m4 macros.

The Sendmail distribution provides the m4 source files necessary to build a Sendmail configuration. The m4 source files are contained in the nine subdirectories of the cf directory. for most configurations, each of the nine subdirectories can be ignored because they are either unused nor they contain source files that are never modified by the system administrator. The only subdirectory that the administrator needs to work with for most config is the cf/cf directory.

The cf/cf directory contains the macro configuration files. The Sendmail administrator creates a macro configuration file that selects the source files that provide the features necessary for the Sendmail configuration. Most macro configuration files are not built from scratch. The Sendmail distribution provides about 20 different sample macro configuration files. You select a macro configuration file that matches your needs and only make small adjustments if they are necessary.

The macro configuration file is then processed through m4 to produce the sendmail.cf file. But even this step may not be necessary if you do not change the sample macro configuration file for your configuration. Several Sendmail configuration files built from sample configuration files are included in the cf/cf directory.

To select and modify the correct m4 macro configuration file, you must have a base understanding of the m4 macro configuration language. Use the tables in this chapter and the list of configuration commands in Appendix A to help you read and modify the macro configuration file.

# The Generic Configuration

The challenge in Chapter 4, "Creating a Basic Configuration," was to find or create sendmail.cf file compatible with Sendmail 8.11. Because the Sendmail 8.11 distribution comes with a file generic-linux that is already in the proper format, the first thing we tried to use generic-linux.cf without modification. The result was this error:

```
[root]# sendmail -v -C:/generic-linux.cf
./generic-linux.cf: line 66: fileclass:
  cannot open '/etc/mail/local-name'
  : No file or directory
```

The generic-linux.mc file that created the generic-linux.cf file has only five significant commands lines:

# **Listing 5** The Commands Contained in generic-linux.mc

```
[craig$ tail -5 generic-linux.mc
VERSIONID$id: generic-linux.mc,v 8.1 1999/09/24 22:48:05 gshapiro Exp $'
OSTYPE(linux)dnl
DOMAIN(generic)dnl
MAILER(local)dnl
MAILER(smtp)dnl
```

We know the VERSIONID macro has no effect other than holding user-defined version control information. We also know that the OSTYPE macro and the two MAILER macros are required for a functioning system. This leads us to guess that removing the DOMAIN macro is the best place to start attacking the problem. Therefore, in Chapter 4 we created a simple m4 configuration file that used it to produce a sendmail.cf file compatible with Sendmail 8.11. It worked, and got Sendmail up and running.

Sometimes a quick solution based on an educated guess is all that you have time for. When you get some free time you are drawn back to the problem to find out why your guess worked and figure out if there is a better long-term solution to the problem. We need to know more about the macro sources called by the generic-linux.mc file in order:

+   - find out how the simple change worked for our problem
-   see if there is a better way to solve our problem
-   find out what features were lost by our quick and dirty solution
-   learn more about configuring Sendmail
