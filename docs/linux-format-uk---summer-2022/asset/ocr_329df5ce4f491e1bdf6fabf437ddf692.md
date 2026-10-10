# **LocAlIsing LiNuX in-DEPTH**

The GCOLIBRI variable is the character variable that tells the system a number of things: the number used to kick off language files for this character set in /usr/lib/locale/POS, any additional files to add to /usr/share/locale and whether or not to use locale data from Koi8-R, PCMSYS, SPC, UK, CP866 or CP1251.

The GCSYMBOL variable is a 24-character symbol representing the locale. Each character in the 24-character string represents a character code. For a given GCSYMBOL, there is an alternate GCOLIBRI variable and a GCSYMBOL variable for every current locale. One of the 24-character strings is an empty string (that is, a string of length zero), and this string represents no GCSYMBOL. All GCSYMBOLs are represented in /usr/lib/locale/gcolibri.

The GCOLIBRI variable is a 24-character string. Each character in the 24-character string represents a character code. For a given GCSYMBOL, there is an alternate GCOLIBRI variable and a GCSYMBOL variable for every current locale. One of the 24-character strings is an empty string (that is, a string of length zero), and this string represents no GCSYMBOL. All GCSYMBOLs are represented in /usr/lib/locale/gcolibri.

+   - To select the language for the first tool, *Select the current default font for this language*. You can select one of four fonts. If you select the font for a current locale, the default is that font for that language. If you select the font for another language, the default is that font for that language.
+   - To select the current default font for this language, *Select the current default font for this language*. You can select one of four fonts. If you select the font for a current locale, the default is that font for that language. If you select the font for another language, the default is that font for that language.

# #### Recognising a locale

A locale is an identifier for a set of symbols that are the standard symbols in one culture. To create a locale, you first define a locale identifier and then define the specific characters, symbols, numbers, date/time formats, and so on, that are used in that culture. This is called a locale definition.

+   - The three standard locales are:
+   	- The C locale.
+   	- The C.utf-8 locale.
+   	- The en_US.UTF-8 locale.
+   - The three standard character sets are:
+   	- US-ASCII
+   	- ISO-8859-1
+   	- ISO-8859-2
+   	- ISO-8859-5
+   	- ISO-8859-7
+   	- ISO-8859-9
+   	- ISO-8859-15
+   	- UTF-8

These three tools can generally work without specifying the system locale, and it is not necessary to use any of the system’s locale settings for them to work. Only environments like the C locale and any languages that are not supported by the system’s locale settings. For example, a system that does not have the Russian locale setting cannot work with the Russian language. The Russian language is not supported by the system’s locale settings.

# # DOUBLE-BYTES: DOUBLE-BYTE!

In the Chinese, Japanese and Korean characters, all three use a double-byte character encoding. In the case of Chinese, for example, it is possible that there are two bytes that represent a character. In other words, there are two bytes that represent a character. In the case of Chinese, there are two bytes that represent a character. In the case of Chinese, there are two bytes that represent a character.