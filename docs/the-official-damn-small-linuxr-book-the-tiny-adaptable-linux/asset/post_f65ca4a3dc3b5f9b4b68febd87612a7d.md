
extensions. All extensions to be shared must be GNU Public License (GPL) or similar license.

There are a couple of additional files needed to participate in the community repositories. The first is an information file. Users will want to browse a summary that describes your extension. This summary is available both via the website of repositories and is also part of the displayed screens when a user selects the MyDSL download browser tool.

## The Info File for All to Read

The `.info` file is a simple text file and is an additional suffix to the extension name. For example, the `zile.dsl` information file is `zile.dsl.info`. Using a text editor such as beaver, create the following file:

```
Title:              zile.dsl
Description:        Zile is an Emacs like text editor
Version:            2.2.29
Author:             http://www.my_program.org/
Original-site:      http://www.my_program.org/
Copying-policy:     GPL
--------------------------------------------------
Extension by:       <your email address>
Comments:           This is an Emacs like text editor.
                    It is a console-based application.
                    It can be run from CLI or X hosted by an aterm.
                    It requires the xxxx.dsl and the yyyy.dsl to function.
                    This was repackaged from my_program_42.0-0_i386.deb
                    found at ftp.us.debian.org woody.
                    Includes icon and menu.
Change-log:         2006/08/24 - First Version
Current:            2007/02/12 - Upgraded and Revised for xxxx-new.dsl
```

The preceding is just an example. In the Comments section, you should include where you got the program. List any other MyDSL extensions that may be required by your extension.

## Checksum File for Quality Assurance

The second file required is a checksum file. This file is mandatory and is part of an automated process when users use the MyDSL download tool. This file ensures that the user has received a good download.

Many things can happen when users are downloading files. Part of the automated download process verifies the checksum and notifies the user if the checksum is different. Users who download via the web are also strongly encouraged to verify checksum before they try to use an extension. The name of this file is the base extension name with a suffix of `.md5.txt`. For your Zile example, it would be `zile.dsl.md5.txt`. To create this file, simply use the md5sum program in DSL to create it for Zile, type the following:

```
# md5sum zile.dsl > zile.dsl.md5.txt
```

## Submitting Your Extension for Publication

The final step is to collect all three files and email them to extensions@damsmallinux.org. For your Zile example, you would send an email with the subject line to contain (at least) the following words: DSL Zile Extension. Then, attach `zile.dsl`, `zile.dsl.info`, and `zile.dsl.md5.txt`.

Submitted extensions are usually processed once a week. Once the extension is processed, a “Thank You” email is sent to you, indicating that the submitted extension is published to the testing area of the MyDSL repository. An announcement is also posted in the DSL forums testing area.

A new topic is created each month for extensions submitted during that month. The announcement alerts the user community to begin testing the new extension. As an extension submitter, you should respond to questions and make corrections when necessary.

If, on the other hand, the submitted extension is missing one of the required files or fails the md5sum integrity check during processing, an email is sent describing what is needed before the extension can be accepted.

## SUMMARY

Adding applications to DSL can be as easy as using Debian Apt system. Because using Apt with DSL is very RAM inefficient, you learned how to create the much more memory efficient MyDSL extensions. You saw that it can be as easy as running two scripts: `deb2dsl` and `dsl2unc`.

You saw that adding menus and icons can be done in easy-to-make text files. You have learned the structure that the MyDSL download tool expects, as well as the structure needed to use the `mydsl-load` command to handle MyDSL desktop icons.

You also saw the more challenging aspects of compiling from source code and creating self-contained applications and how to package the most powerful type of MyDSL extension: the uci.

Overall, MyDSL extensions are just repackaged files and directories together with some common elements to support the live CD-ROM single user environment of DSL.
