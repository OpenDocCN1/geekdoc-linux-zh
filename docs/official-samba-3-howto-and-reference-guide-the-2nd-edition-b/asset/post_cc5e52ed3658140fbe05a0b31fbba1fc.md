
One standardized multibyte charset encoding scheme is known as **Unicode**². A big advantage of using a multibyte charset is that you only need one. There is no need to make sure two computers use the same charset when they are communicating.

Old Windows clients use single-byte charsets, named *codepages*, by Microsoft. However, there is no support for negotiating the charset to be used in the SMB CIFS protocol. Thus, you have to make sure you are using the same charset when talking to an older client. Newer clients (Windows NT, 2000, XP) talk Unicode over the wire.

### 29.3 Samba and Charsets

As of Samba-3, Samba can (and will) talk Unicode over the wire. Internally, Samba knows of three kinds of character sets:

- **_unix charset_**: This is the charset used internally by your operating system. The default is `UTF-8`, which is fine for most systems and covers all characters in all languages. The default in previous Samba releases was to *save filenames in the encoding of the clients* — for example, `CP850` for Western European countries.
- **_display charset_**: This is the charset Samba uses to print messages on your screen. It should generally be the same as the _unix charset_.
- **_dos charset_**: This is the charset Samba uses when communicating with DOS and Windows 9x ME clients. It will talk Unicode to all newer clients. The default depends on the charsets you have installed on your system. Run `testparm -v | grep "dos charset"` to see what the default is on your system.

### 29.4 Conversion from Old Names

Because previous Samba versions did not do any charset conversion, characters in filenames are usually not correct in the UNIX charset but only for the local charset used by the DOS/Windows clients.

Bjoern Jiaekle has written a utility named **convmv**³ that can convert whole directory structures to different charsets with one single command.

### 29.5 Japanese Charsets

Setting up Japanese charsets is quite difficult. This is mainly because:

- The Windows character set is extended from the original legacy Japanese standard (JIS X 0208) and is not standardized. This means that the strictly standardized implementation cannot support the full Windows character set.
- Mainly for historical reasons, there are several encoding methods in Japanese, which are not fully compatible with each other. There are two major encoding methods. One is the Shift_JIS series used in Windows and some UNIXes. The other is the EUC-JP series used in most UNIXes and Linux. Moreover, Samba previously also offered several unique encoding methods, named CAP and HEX, to keep interoperability with CAP/NetAtalk and UNIXes that can't use Japanese filenames. Some implementations of the EUC-JP series can't support the full Windows character set.
- There are some code conversion tables between Unicode and legacy Japanese character sets. One is compatible with Windows, another one is based on the reference of the Unicode consortium, and others are a mixed implementation. The Unicode consortium does not officially define any conversion tables between Unicode and legacy character sets, so they cannot be standard one.
- The character set and conversion tables available in `iconv()` depend on the iconv library that is available. Next to that, the Japanese locale names may be different on different systems. This means that the value of the charset parameters depends on the implementation of `iconv()` you are using.

Though 2-byte fixed UCS-2 encoding is used in Windows internally, Shift_JIS series encoding is usually used in Japanese environments as ASCII encoding is in English environments.

### 29.5.1 Basic Parameter Setting

The `dos charset` and `display charset` should be set to the locale compatible with the character set and encoding method used on Windows. This is usually CP932 but sometimes has a different name.

The `unix charset` can be either Shift_JIS series, EUC-JP series, or UTF-8. UTF-8 is always available, but the availability of other locales and the name itself depends on the system.

Additionally, you can consider using the Shift_JIS series as the value of the `unix charset` parameter by using the `vfs.cap` module, which does the same thing as setting “coding system = CAP” in the Samba 2.2 series.

Where to set `unix charset` to is a difficult question. Here is a list of details, advantages, and disadvantages of using a certain value.

**Shift_JIS series**

Shift_JIS series means a locale that is equivalent to Shift_JIS, used as a standard on Japanese Windows. In the case of Shift_JIS, for example, if a Japanese filename consists of 0x88a4 and 0x974e (a 4-bytes Japanese character string meaning “share”) and “.txt” is written from Windows on Samba, the filename on UNIX becomes 0x88a4, 0x974e, “.txt” (an 8-byte BINARY string), same as Windows.

Since *Shift_JIS* series is usually used on some commercial-based UNIXes: hp-ux and AIX as the Japanese locale (however, it is also possible to use the EUC-JP locale series). To use *Shift_JIS* series on these platforms, Japanese filenames created from Windows can be referred to also on UNIX.

If your UNIX is already working with *Shift_JIS* and there is a user who needs to use Japanese filenames written from Windows, the *Shift_JIS* series is the best choice. However, broken filenames may be displayed, and some commands that cannot handle non-ASCII filenames may be aborted during parsing filenames. Especially, there may be “\” (0x5c) in filenames, which need to be handled carefully. It is best to not touch filenames written from Windows on UNIX.

Note that most Japanized free software actually works with EUC-JP only. It is good practice to verify if the Japanized free software can work with *Shift_JIS*.

**EUC-JP series**

EUC-JP series means a locale that is equivalent to the industry standard called EUC-JP, widely used in Japanese UNIX (although EUC contains specifications for languages other than Japanese, such as EUC-KR). In the case of EUC-JP series, for example, if a Japanese filename consists of 0x8ba4 and 0x974c and “.txt” is written from Windows on Samba, the filename on UNIX becomes 0xb6a6, 0xcedd: “.txt” (an 8-byte BINARY string).

Since EUC-JP is usually used on open source UNIX, Linux, and FreeBSD, and on commercial-based UNIX, Solaris, IRIX, and Tru64 UNIX as Japanese locale (however, it is also possible on Solaris to use *Shift_JIS* and UTF-8, and on Tru64 UNIX it is possible to use *Shift_JIS*). To use EUC-JP series, most Japanese filenames created from Windows can be referred to also on UNIX. Also, most Japanized free software works mainly with EUC-JP only.

It is recommended to choose EUC-JP series when using Japanese filenames on UNIX. Although there is no character that needs to be carefully treated like “\” (0x5c), broken filenames may be displayed and some commands that cannot handle non-ASCII filenames may be aborted during parsing filenames.

Moreover, if you built Samba using differently installed libconv, the `eucJP-ms` locale included in libconv and EUC-JP series locale included in the operating system may not be compatible. In this case, you may need to avoid using incompatible characters for filenames.

**UTF-8**

UTF-8 means a locale equivalent to UTF-8, the international standard defined by the Unicode consortium. In UTF-8, a character is expressed using 1 to 3 bytes. In case of the Japanese language, most characters are expressed using 3 bytes. Since on Windows *Shift_JIS*, where a character is expressed with 1 or 2 bytes, is used to express Japanese, basically a byte length of a UTF-8 string is 1.5 times that of the original *Shift_JIS* string. In the case of UTF-8, for example, if a Japanese filename consists of 0x8ba4 and 0x974c, and “.txt” is written from Windows on Samba, the filename on UNIX becomes 0xe585, 0xb1b6, 0x9e89: “.txt” (a 10-byte BINARY string).

> ² <http://www.unicode.org/>  
> ³ <default://j3se.de/linux/convmv/>
