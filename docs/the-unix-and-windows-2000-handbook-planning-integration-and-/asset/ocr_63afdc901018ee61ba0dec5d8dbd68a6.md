configuration file that will call other macro files from the domain, feature, hack, mailer, and ostype directories:

+   ```text
+   domain        hack          mailer        sh
+   cf            feature       m4            ostype        siteconfig
+   ```

We will create files in the cf and domain directories to generate an example sendmail.cf file. The first step is to change into the domain directory. This directory will contain files with the m4 suffix. Copy the generic.m4 file, changing its name to your domain, such as example.com.m4. The new file is displayed in Listing 9.1. We will now examine the file we have just created.

divert(-1) (minus one) line signals m4 to suppress output, which excludes comments from being added to the sendmail.cf file. divert(0) signals m4 to resume regular output. The next few lines contain macros and definitions that will be added to the sendmail.cf file. This file should be used to specify macros, options, and definitions that may be required for this particular mail host. The define line configures the search path that Sendmail will traverse for a user's .forward file.

The next line, FEATURE(redirect)dnl, bounces mail back to the sender with the message 551 User not local : please try <newaddress> when the REDIRECT option is used in the alias file. The flexibility of m4 allows FEATURE lines to be included in the master configuration file or the domain configuration file. There are approximately 30 features that can be specified. The README file, located in the cf directory, contains a complete listing of these features and their definitions. Best practice is to place all of the FEATURE lines in one configuration file.

The final line instructs Sendmail to read the /etc/sendmail.cf file. The sendmail.cf file contains hostnames that the local mail machine will interpret as its own name. The sendmail.cf file performs a mail alias function. The README file in the top level of the cf directory provides a complete listing of all macros, options, and definitions valid for the .m4 domain file.

```
```text
divert(-1)
#
# Copyright (c) 1998 Sendmail, Inc.  All rights reserved.
# Copyright (c) 1983 Eric P. Allman.  All rights reserved.
# Copyright (c) 1988, 1993.
#        The Regents of the University of California.  All rights reserved.
#
# By using this file, you agree to the terms and conditions set
# forth in the LICENSE file.
divert(-1)
#
```
```