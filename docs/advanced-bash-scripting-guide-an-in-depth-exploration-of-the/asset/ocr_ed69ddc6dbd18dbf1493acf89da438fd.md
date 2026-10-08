# Advanced Bash-Scripting Guide

1. understands the gettext and eval_gettext commands (whereas bash --dump-po-strings understands only its deprecated $") syntax

2. can extract comments by the programmer, intended to be read by the translator.

This shell code is not specific to Bash any more; it works the same with Bash l x and other /bin/sh implementations.

Now, build a language.po file for each language that the script will be translated into, specifying the msgstr. Alfredo Pironti gives the following example:

fr.po:

```
# a:6
msgid "Can't cd to $var."
msgstr "Impossible de se positionner dans le repertoire $var."
# a:7
msgid "Enter the value: "
msgstr "Entrez la valeur : ""

# The string is dumped with the variable names, not with the %s syntax,
+# similar to C programs.
+# This is a very cool feature if the programmer uses
#+ variable names that make sense!
```

Then, run msgfmt.

msgfmt -o localized.sh fr po

Placing the localized.sh file in the /usr/local/share/locale/fr/LC_MESSAGES directory, and at the beginning of the script, insert the lines:

```
TEXTDOMAIN=/usr/local/share/locale
TEXTDOMAIN-localized.sh
```

If a user on a French system runs the script, she will get French messages.

> With older versions of Bash or other shells, localization requires gettext, using the -s option. In this case, the script breaks:

```
#!/bin/bash
# localized.sh

_CDERROR=65

error() {
  local format=$1
  shift
  printf "$(gettext -s $format) "$@" >&2
  exit $E_CDERROR
}

cd var "Can't cd to %s." "$var"
read -p "$(gettext -s "Enter the value: ")" var\...
```

The TEXTDOMAIN and TEXTDOMAIN variables must be set and exported to the environment. This should be done within the script itself.

Appendix K. Localization