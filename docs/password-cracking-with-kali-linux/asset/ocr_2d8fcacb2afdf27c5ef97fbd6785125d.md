![](bbox=[0.13, 0.09, 0.87, 0.29])

When using Hashcat you need to tell it a few things:

+   * Type of password hash
+   * Filename of the file containing the un-cracked hashes
+   * The Dictionary or Wordlist filename
+   * The Output filename to store the cracked hashes
+   * And finally, the attack mode type and switches for any other options you want

The most basic use of Hashcat is to use a single wordlist file.

# Example:

```
`hashcat --remove -m 0 [Uncracked].txt wordlist.txt -o [Cracked.txt] -O`
```

I always use the "--remove" switch when cracking with Hashcat. This tells Hashcat to remove any cracked word from the uncracked wordlist. If you don’t, it will keep it in the uncracked wordlist, lengthening cracking times. You must also provide Hashcat the correct hash type. The "-m 0" is the hash type that you will be attempting to crack. In the example, the "0" specifies that the hashes are MD5. Hashcat is able to crack a wide range of hashes. These are listed by using the "hashcat --help" command.

An abbreviated list of supported -m Hash types: