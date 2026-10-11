+   • The Windows character set is extended from the original legacy Japanese standard (JIS X 0208) and is not standardized. This means that the strictly standardized implementation cannot support the full Windows character set.
+   
+   • Mainly for historical reasons, there are several encoding methods in Japanese, which are not fully compatible with each other. There are two major encoding methods. One is the Shift_JIS series used in Windows and some UNIXes. The other is the EUC-JP series used in most UNIXes and Linux. Moreover, Samba previously also offered several unique encoding methods, named CAP and HEX, to keep interoperability with CAP/NetAtalk and UNIXes that can't use Japanese filenames. Some implementations of the EUC-JP series can't support the full Windows character set.
+   
+   • There are some code conversion tables between Unicode and legacy Japanese character sets. One is compatible with Windows, another one is based on the reference of the Unicode consortium, and others are a mixed implementation. The Unicode consortium does not officially define any conversion tables between Unicode and legacy character sets, so they cannot be standard one.
+   
+   • The character set and conversion tables available in iconv() depend on the iconv library that is available. Next to that, the Japanese locale names may be different on different systems. This means that the value of the charset parameters depends on the implementation of iconv() you are using.

Though 2-byte fixed UCS-2 encoding is used in Windows internally, Shift_JIS series encoding is usually used in Japanese environments as ASCII encoding is in English environments.

# 29.5.1 Basic Parameter Setting

The dos charset and display charset should be set to the locale compatible with the character set and encoding method used on Windows. This is usually CP932 but sometimes has a different name.

The unix charset can be either Shift_JIS series, EUC-JP series, or UTF-8. UTF-8 is always available, but the availability of other locales and the name itself depends on the system.

Additionally, you can consider using the Shift_JIS series as the value of the unix charset parameter by using the vfs.cap module, which does the same thing as setting “coding system = CAP” in the Samba 2.2 series.

Where to set unix charset to is a difficult question. Here is a list of details, advantages, and disadvantages of using a certain value.

Shift_JIS series Shift_JIS series means a locale that is equivalent to Shift_JIS, used as a standard on Japanese Windows. In the case of Shift_JIS, for example, if a Japanese filename consists of 0x88a4 and 0x974e (a 4-bytes Japanese character string meaning “share”) and ““.txt” is written from Windows on Samba, the filename on UNIX becomes 0x88a4, 0x974e, ““.txt” (an 8-byte BINARY string), same as Windows.