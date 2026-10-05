```
kali@kali:~/passwordattacks$ sed -i '^/1/d' demo.txt
```

```
kali@kali:~/passwordattacks$ cat demo.txt
password
iloveyou
princess
rockyou
abc123
```

Listing 266 - Contents and location of demo.txt

We now have five passwords in our demo.txt wordlist. Let's mutate these passwords to fit the password policy, which must include a numerical value, a special character, and an uppercase letter.

The Hashcat Wiki<sup>229</sup> provides a list of all possible rule functions. If we want to add a character, the simplest form is to prepend or append it. We can use the $ function to add a character or ^ to prepend a character. Both of these expect one character after the function selector. For example, if we want to append "3" to every password in a file, the corresponding rule function would be *3.

When generating a password with a numerical value, many users simply add a "1" at the end of an existing password. Therefore, let's create a rule file containing $1 to add to all passwords in our wordlist. We'll create a demo.rule with this function rule. We will need to escape the special character "S" to echo it into the file correctly.

```
kali@kali:~/passwordattacks$ echo \$1 > demo.rule
```

Listing 267 - Rule function to add a '1' to all passwords

Now, we can use hashcat with our wordlist, providing the rule file with -r, and -stdout, which starts Hashcat in debugging mode. In this mode, Hashcat will not attempt to crack any hashes, but may display the mutated passwords.

```
kali@kali:~/passwordattacks$ hashcat -r demo.rule --stdout demo.txt
password1
iloveyou
princess1
rockyou
abc123
```

Listing 268 - Using Hashcat in debugging mode to display all mutated passwords

The list shows that a "1" was appended to each password by the rule $1.

> If you receive the error "Not enough allocatable device memory for this attack", shut down your Kali VM and add more RAM to it. 4GB is enough for the examples and exercises.