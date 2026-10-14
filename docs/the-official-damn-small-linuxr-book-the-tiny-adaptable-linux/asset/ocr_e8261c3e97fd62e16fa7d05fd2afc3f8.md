base extension name with a suffix of `.md5.txt`. For your Zile example, it would be `zile.dsl.md5.txt`. To create this file, simply use the md5sum program in DSL to create it for Zile, type the following:

```
# md5sum zile.dsl > zile.dsl.md5.txt
```

# Submitting Your Extension for Publication

The final step is to collect all three files and email them to extensions@damsmallinux.org. For your Zile example, you would send an email with the subject line to contain (at least) the following words: DSL Zile Extension. Then, attach `zile.dsl`, `zile.dsl.info`, and `zile.dsl.md5.txt`.

Submitted extensions are usually processed once a week. Once the extension is processed, a “Thank You” email is sent to you, indicating that the submitted extension is published to the testing area of the MyDSL repository. An announcement is also posted in the DSL forums testing area.

A new topic is created each month for extensions submitted during that month. The announcement alerts the user community to begin testing the new extension. As an extension submitter, you should respond to questions and make corrections when necessary.

If, on the other hand, the submitted extension is missing one of the required files or fails the md5sum integrity check during processing, an email is sent describing what is needed before the extension can be accepted.

# SUMMARY

Adding applications to DSL can be as easy as using Debian Apt system. Because using Apt with DSL is very RAM inefficient, you learned how to create the much more memory efficient MyDSL extensions. You saw that it can be as easy as running two scripts: `deb2dsl` and `dsl2unc`.

You saw that adding menus and icons can be done in easy-to-make text files. You have learned the structure that the MyDSL download tool expects, as well as the structure needed to use the `mydsl-load` command to handle MyDSL desktop icons.

You also saw the more challenging aspects of compiling from source code and creating self-contained applications and how to package the most powerful type of MyDSL extension: the uci.

Overall, MyDSL extensions are just repackaged files and directories together with some common elements to support the live CD-ROM single user environment of DSL.