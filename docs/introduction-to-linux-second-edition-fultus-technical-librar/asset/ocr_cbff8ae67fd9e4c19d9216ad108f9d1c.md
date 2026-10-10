# Introduction to Linux

For setting the time zone correct, you can use **tzconfig** or **timezone** commands. Timezone information is usually set during the installation of your machine. Many systems have distribution-specific tools to configure it, see your system documentation.

# 7.4.4 Language

If you'd rather get your messages from the system in Dutch or French, you may want to set the LANG and LANGUAGE environment variables, thus enabling locale support for the desired language and eventually the fonts related to character conventions in that language.

With most graphical login systems, such as **gdm** or **kdm**, you have the possibility to configure these language settings before logging in.

Note that on most systems, the default tends to be en_US.UTF-8 these days. This is not a problem, because systems where this is the default, will also come with all the programs supporting this encoding. Thus, vi can edit all the files on your system, cat won't behave strange and so on.

Trouble starts when you connect to an older system not supporting this font encoding, or when you open a *UTF-8* encoded file on a system supporting only 1-byte character fonts. The recode utility might come in handy to convert files from one character set to another. Read the man pages for an overview of features and usage. Another solution might be to temporarily work with another encoding definition, by setting the LANG environment variable:

```
debby:-> acroread /var/tmp/514348.pdf
Warning: charset "UTF-8" not supported, using "ISO8859-1".
Aborted

debby:-> set | grep UTF
LANG=en_US.UTF-8

debby:-> export LANG=en_US

debby:-> acroread /var/tmp/514348.pdf
<--new window opens-->
```

Refer to the Mozilla <http://www.mozilla.org/> web site for guidance on how to get Firefox in your language. The OpenOffice.org <http://www.openoffice.org/> web site has information on localization of your OpenOffice.org suite.

# 7.4.5 Country-specific Information

The list of HOWTOs <http://www.tldp.org/HOWTO/HOWTO-INDEX/howtos.html> contains references to Bangla, Belarusian, Chinese, Esperanto, Finnish,