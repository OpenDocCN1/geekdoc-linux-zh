![](bbox=[0.14, 0.07, 0.87, 0.54])

Figure 7.1  Juana’s portion of the RFI directory structure.

# **Example 7.6 An Exception to the Exception to**
**Asterisk (\*) Wildcard Expansion**

Upon receiving the call for help (see Example 7.2), Preston advises Perez to enter the following in his home directory:

```
$ echo .bash* <Enter>
.bash_history .bash_logout .bash_profile .bashrc
```

Perez is rewarded by a listing of the names of all his hidden .bash files.

# **The Question Mark as a Wildcard**

A question mark (? ) is another wildcard that you can use in a filename specification. The shell substitutes filenames that have only a single character in the same position as the question mark, as shown in Example 7.4.