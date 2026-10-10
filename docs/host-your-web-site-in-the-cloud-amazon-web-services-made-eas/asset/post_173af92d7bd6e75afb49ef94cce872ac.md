
Start by visiting http://aws.amazon.com and click on the button labeled **Sign Up Now**, as shown in Figure 3.9.

![](img/4a5ba0dd041e08e6a67fa31d52309995_78_0.png)

On the next page, enter your email address and select the **I am a new user** option, then click on the **Sign in using our secure server** button. Proceed to the registration page. Fill in your name, enter your email address a second time (for verification), choose a secure password, and click on the **Create account** button.

Enter your contact information (including your street address) on the next page. Then scroll down a bit so that the AWS license agreement is visible. Read all the fine print and check the checkbox to indicate that you’ve read and agree to the terms of the license. Scroll down some more and enter the security check code, and click the **Continue** button.

![](img/4a5ba0dd041e08e6a67fa31d52309995_78_1.png)

Once you’ve done this, you’ll see a page like the one shown in Figure 3.10, indicating that you now have an AWS account. Congratulations, and welcome to the club!

There’s still a little more left to do, though. We’ve yet to reach the part where you enter your credit card number. The next step is to sign up for an actual AWS service. Click on the Amazon Elastic Compute Cloud button, and then click on the Sign Up For Amazon EC2 button. You may need to enter your email address and password to access the next page.

The next page includes complete pricing information on EC2 services and S3; you need to use S3 to store your Amazon Machine Images, so this form covers both. Review the pricing information, then scroll down to the bottom of the page and enter your credit card information. Click the Continue button and on the next page, select Use This Address if the address you already entered is also the billing address for your credit card. Otherwise, enter the appropriate address and click on the Continue button. Finally, scroll down to the bottom of the confirmation page and click on the Complete Sign Up button.

You’ll see the “Thank you for signing up . . .” page and a notice informing you that you’ll receive a sequence of confirmation emails after the sign-up process:

- 1. the “Welcome to Amazon” email that indicates that you now have an Amazon account
- 2. the “Welcome to AWS” email that indicates that you now have an AWS account
- 3. the final pair of emails indicating that you’ve signed up for EC2 services and S3

## Obtaining Your AWS Keys

Once you’ve created an AWS account, the next step is to access your public and private AWS keys.

Go to the AWS portal at http://aws.amazon.com and select Security Credentials from the Account menu, as shown in Figure 3.11.

![](img/4a5ba0dd041e08e6a67fa31d52309995_80_0.png)

Figure 3.11. Account menu

Enter your email address and password again if necessary. You’ll now see the **Security Credentials** page. Scroll down to find the section labeled **Your Access Keys**, as shown in Figure 3.12.

| Created | Access Key ID | Secret Access Key | Status |
| --- | --- | --- | --- |
| September 10, 2009 | AKIAIPR3EIIJ36PMQQVST | Show | Active (Make Inactive) |

Create a New access Key

Figure 3.12. Your Access Keys

You’re going to need this key in the next section, so select your **Access Key ID** and then copy and paste it into a scratch file (Notepad or TextEdit is always good for this).

Now click on the **Show** link to see your **Secret Access Key**, like the one shown in Figure 3.13. Again, select it, copy it, and paste it to your scratch file.

![](img/4a5ba0dd041e08e6a67fa31d52309995_80_1.png)

Figure 3.13. The Secret Access Key

With this information in hand, you’re all set to download and install CloudFusion in the next section.

## Running the PHP Code in This Book

All the code in this book is PHP code. We’ll be running PHP on the command line and on a web server. Along with the book’s assumption about your PHP knowledge, is the assumption that you can install and run PHP and a web server on your specific platform. However, there’s just enough room in this chapter to provide a nudge in the right direction.

If you use Windows, look no further than the WampServer package 30 to have you up and running in no time at all. Similarly, MAMP 31 is a one-click installer for Mac OS X. Most Linux distributions already have Apache and PHP installed, but they’re also available via your distribution’s package manager. If you need more information, have a look at Chapter 1 of Kevlin Yank’s book Build Your Own Database Driven Web Site Using PHP and MySQL, freely available on sitepoint.com. 32

> **GD Not Included in Mac OS X**
>
> Some of the code in the next chapter makes extensive use of PHP’s GD library 33 for image manipulation. Unfortunately, while PHP is included as part of Mac OS X, the GD extension is excluded. To remedy this situation you can either use MAMP, mentioned above, or install the Mac OS X PHP package linked from the PHP web site under the heading **Binaries for other systems**. 34

We’re about to get serious with PHP, but before we do I have to mention this vital information. The PHP programs in this book that commence with a shebang (`#!/usr/bin/php`) are meant to be run from the command line, for example:

```
#!/usr/bin/php
<?php

: php script

?>
```

30 http://www.wampserver.com/en/
31 http://www.mamp.info/
32 http://articles.sitepoint.com/article/php-amp-mysql-1-installation/
33 http://www.php.net/gd/
34 http://www.php.net/downloads.php

Running PHP scripts from the command line takes the form:

```
$ path_to_php_executable php_script_file [php_script_arguments]
```

The $ in this example represents the command prompt and is not typed in. Here’s an example of running a PHP script on a Linux machine:

```
$ /usr/bin/php list_buckets.php
```

Here’s another example, this time on a Mac OS X machine using MAMP:

```
$ /Applications/MAMP/bin/php5/bin/php list_buckets.php
```

Here’s an example of running these scripts on a Windows machine from the Windows Command Prompt:

```
C:\> C:\PHPS\php list_buckets.php
```

Further details about running PHP from the Windows command line can be found in the PHP Manual.²⁵

## Running PHP as a Shell Script

If you’re running these scripts on a Linux or Mac OS X machine you can run them like a shell script, but you need to make the files executable first. You can do so using the `chmod` command:

```
$ chmod +x list_buckets.php
```

After doing that you can run your scripts like so:

```
$ ./list_buckets.php
```

In order for this to work, the shebang line in all your scripts must indicate the location of the PHP executable on your system.

Scripts that are meant to be run on your web server will have no shebang:

```
<?php
: php script
?>
```

## PHP 5.3.0 and Time Zones

If you’re using PHP 5.3.0, there is an important change from previous versions. PHP 5.3.0 will now issue a warning-level log message whenever you use a date-related function without specifying a time zone. PHP has always defaulted to the time zone of the machine it’s running on, but that behavior is now deemed to be unreliable and so the warning is emitted.

To avoid seeing the warning messages you must specify a time zone when using date functions, or else set a default time zone. 36 The easiest way to set a default time zone is to edit your **php.ini** file, specifically the following line:

```
; Defines the default timezone used by the date functions
date.timezone =
```

Uncomment the line and add a valid time zone value. You can find a list of time zone values on the PHP web site. 37 Here’s an example:

```
; Defines the default timezone used by the date functions
date.timezone = America/Los_Angeles
```

## Installing CloudFusion

Many of the examples in this book can be run locally—that is, from your PHP-equipped desktop machine running Windows, Mac OS, or Linux—or remotely on a server or an EC2 instance. Wherever you plan to run them from, that’s where you’ll need to install CloudFusion. Here are the steps involved:

- 1. As at the time of writing, the latest version of CloudFusion was 2.5. You can download it from the project’s web site at http://getcloudfusion.com. Unzip

36 http://www.php.net/manual/en/migration52.datetime.php
37 http://www.php.net/manual/en/timezones.php
