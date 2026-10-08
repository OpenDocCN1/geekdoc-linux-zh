# 254 LOCALIZATION

message consists of text that contains 8-bit characters from the ISO-8859-1ncharacter set.

```
Mime-Version: 1.0
Content-Type: text/plain; charset=iso-8859-1
Content-Transfer-Encoding: 8bit
```

If the transport route is not 8-bit clean, you can either substitute special characters with replacement characters or sequences of characters (which is a rather outmoded way of doing things), or you leave their encoding to a MIME-capable¹ program which provides conversion in a completely transparent way to the user. However, this procedure only works without problems if both partners use MIME-capable programs.

MIME is rapidly becoming a standard, in particular many Windows programs create such messages by default. It is only a question of time until important programs under UNIX will also be capable of coping with MIME more or less.

# 9.6.1 The mail reader elm

The program elm is an easy-to-use, but nevertheless powerful, mail user agent. In the first place, elm must be compiled correctly, which was not the case for long time in the Slack distribution. This allows special characters in incoming messages to be displayed by means of the built-in pager. Furthermore, the above-mentioned header lines can be included automatically with outgoing messages.

```
# elm.rc
# Transport of special characters
charset = iso-8859-1
displaycharset= iso-8859-1
extencoding = 8bit
pager = builtin
```

However, elm can also cooperate with the MIME implementation metamail, so that MIME messages can also be sent.