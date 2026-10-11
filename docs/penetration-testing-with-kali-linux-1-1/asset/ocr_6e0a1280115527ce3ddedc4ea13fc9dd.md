For the sake of this simple demonstration, we will assume that Megacorp One policy dictates that a password end in a two-digit number.

To create passwords that meet this requirement, we could write a Bash script. However, we will instead use a much more powerful tool called John the Ripper (JTR),⁵⁵⁵ which is a fast password cracker with several features including the ability to generate custom wordlists and apply rule permutations.

Moving forward with our assumption about the password policy, we will add a rule to the JTR configuration file (/etc/john/john.conf) that will mutate our wordlist, appending two digits to each password. To do this, we must locate the $List.Rules:Wordlist$ segment where wordlist mutation rules are defined, and append a new rule. In this example, we will append the two-digit sequence of numbers from (double) zero to ninety-nine after each word in our wordlist.

We will begin this rule with the $ character, which tells John to append a character to the original word in our wordlist. Next, we specify the type of character we want to append, in our case we want any number between zero and nine ($0-9$). Finally, to append double-digits, we will simply repeat the $[0-9]$ sequence. The final rule is shown in Listing 592.

```
kali@kali:~$ sudo nano /etc/john/john.conf
 ...
# Wordlist mode rules
[List.Rules:Wordlist]
# Try words as they are
 :
# Lowercase every pure alphanumeric word
-c >3 !?X l Q
# Capitalize every pure alphanumeric word
-c (?a >2 !?X c Q
# Lowercase and pluralize pure alphabetic words
 ...
# Try the second half of split passwords
-s x_
-s-c x_ M l Q
# Add two numbers to the end of each password
$[0-9]$[0-9]
...
```

# Listing 592 · Creating mutation rule in John the Ripper configuration file

> The rules syntax for John the Ripper is quite extensive and powerful, but beyond the scope of this module. For more information, take time to review the rules documentation.⁵⁵⁶

Now that the rule has been added to the configuration file, we can mutate our wordlist, which currently contains 312 entries.

+   ⁵⁵⁵ (Openwall, 2018), http://www.openwall.com/john/
+   ⁵⁵⁶ (Solar Designer, 2017), http://www.openwall.com/john/doc/RULES.shtml