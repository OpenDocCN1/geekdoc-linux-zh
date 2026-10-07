# REDIRECT

> D

P holds the list of pseudo-domains. As explained earlier, pseudo-domains are not real domains found in the DNS; they are used to request special processing from Sendmail. The dot is always defined as part of this class. The value REDIRECT is added because the redhat.mc file built this sendmail.cf file contained the FEATURE(redirect) command. The CPREDICT command in sendmail1.cf clearly demonstrates the direct impact that the macro configuration you build has on the Sendmail configuration.

The third C command assigns the values @, %, and ! to the class variable O. Class O holds tokens that are used to divide the parts of an e-mail address. These three characters cannot be used in local usernames, because they have special meanings in e-mail addresses. Everyone is familiar with the role @ plays in an address. Those who are familiar with UUCP know that ! is used in traditional UUCP banging addressing. And the % character is used in old systems as a way to forward an e-mail address to a remote system for processing. These are default values set by Sendmail that do not need to be modified.

The next two C commands,, and [[ are unique for two reasons. First, demonstrate that variables can be given names that are special characters. Here we are assigning values to the class variable . and to the class variable [ . Secondly, and more surprisingly, the command assigns these variables a value that exactly matches the name of the variable. Thus . is assigned the value . and [ is assigned the value [. We know from the discussion of the D command variables that can be used in pattern matching. Class variables are only used in pattern matching. So why create a variable for and [ when a pattern match could just as easily compare against the literal value? There reasons.

Special symbols are used when referring to classes in a pattern. Above, we saw that the value in an individual variable is referred to as $, where x is the variable name. The $ symbol marks any value in a class, and the ~ symbol marks not any value in a class. Thus $~P means any value in class P and ~ means anything that is not in class.

One reason to define classes named . and [ is that they are expandable. The characters and [ character separates the parts of a domain name. The | character encloses raw IP addresses that are being used in place of hostnames in e-mail addresses. Classes allow Sendmail to compare a variable against a list of values, instead of a single value. This means that if the range of possible characters that can be used to separate domain names ever increases or the range of characters used to

![](bbox=[0.142, 0.935, 0.47, 0.958])