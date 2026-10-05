# Chapter 7 The sendmail.cf File

:

REDIRECT

^D

P holds the list of pseudo-domains. As explained earlier, the value REDRECT is not real domains found in the DNS; they are used to request special processing from Sendmail. The value is always defined as part of this class. The value REDRECT is added because the redhat.mc file used by this sendmail.cf contained the FEATURE(redirect) command. The CPDIRECT command in sendmail.cf file clearly demonstrates the direct impact that the macro configuration you have on the Sendmail configuration.

The third C command assigns the values @, %, and ! to the class variable O. Class O holds tokens that are used to divide the parts of an e-mail address. These three values are characters that cannot be used in local usernames, because they have special meanings in email addresses. Everyone is familiar with UUCP known that ! is used in traditional UUCP bad addressing. The % character is used in old systems as a value to forward an e-mail address to a remote system for processing. These are default values by Sendmail that do not need to be modified.

The two C commands, ., and [[ are unique for two reasons. First, variables can be given names that are special characters. Here we are assigning values to the class variable . and to the class variable [. Secondly, and more surprisingly, the commands assign these variables a value that exactly matches the name of the variable. This variable is assigned the value . and variable [ is assigned the value [. Strange! We know from the discussion of the D command that can be used in pattern matching. Class variables are only used in pattern matching. Why create a variable for . and [ when a pattern match could just easily compare against the literal value? There are reasons.

Special symbols are used when referring to classes in a pattern. Above, we say that the value in an individual variable is referred to as $, where x is the variable name. The $= symbol matches any value in a class and the $ symbol matches not value in a class. Thus $=P means a value in class P and $~ anything that is not in class [.

One reason to define class names. and [ and ] have special meaning in addresses. The . character separates the parts of a domain name. The [ character encloses IP addresses that are being used in place of hostnames in e-mail addresses. Classes allow Sendmail to compare a value against a list of values, instead of against a single value. This means that if the range of possible characters never increases or the range of characters used to be