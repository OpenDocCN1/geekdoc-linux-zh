**Task 2:**
If you're feeling daring (this is not recommended), you can use `update-locale` to change your settings to a radically different language and/or character map. For example, `sudo update-locale LANG=<setting>`

`LANG=C` is notable for being useful in scripting -- it disables localization and uses the default language so that output is consistent.

**Notes:**
You can use `iconv` to convert text between character encodings.