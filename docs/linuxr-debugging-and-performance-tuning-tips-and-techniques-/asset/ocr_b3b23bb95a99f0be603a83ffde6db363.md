# 13.3.2  Translating Messages: gettext()

The next step after setting the text domain is to use the `gettext()` function (or a variant) for every string that should be translated. Several functions provide translation services:

```
#include <libintl.h> `//` **GLIBC**
char *`gettext`(const char *`msgid`);
char *`dgettext`(const char *`domainname`, const char *`msgid`);
char *`dcgettext`(const char *`domainname`, const char *`msgid`, int `category`);
```

The arguments used in these functions are as follows:

+   - `const char *msgid`
+     The string to be translated. It acts as a key into a database of translations.
+   - `const char *domainname`
+     The text domain from which to retrieve the translation. Thus, even though `main()` has called `textdomain()` to set the application’s own domain, messages can be retrieved from other text domains. (This is most applicable to messages that might be in the text domain for a third-party library, for example.)
+   - `int category`
+     One of the domain categories described earlier (`LC_TIME`, etc.).

The default text domain is whatever was set with `textdomain()` (“messages” if `textdomain()` was never called). The default category is `LC_MESSAGES`. Assume that `main()` makes the following call:

```
`textdomain`(“killerapp”);
```

Then, `gettext`(“my message”) is equivalent to `dgettext`(“killerapp”, “my message”). Both of these, in turn, are equivalent to `dcgettext`(“killerapp”, “my message”, `LC_MESSAGES`).

You will want to use `gettext()` 99.9 percent of the time. However, the other functions give you the flexibility to work with other text domains or locale categories. You are most likely to need this flexibility when doing library programming, since a standalone library will almost certainly be in its own text domain.

All the functions return a string. The string is either the translation of the given `msgid` or, if no translation exists, the original string. Thus, there is always some output, even if it’s just the original (presumably English) message. For example: