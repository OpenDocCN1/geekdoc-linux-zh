By using the | operator, this command also works as a filter in cases where the input comes from the output of another UNIX command. For example, the following command sends the output of the cat command to tr:

```
cat names | tr -s ":" " "
```

This sample command sends the contents of the names file to tr. The tr utility replaces each occurrence of the : character with a space. The tr utility works like the sed command, except that sed changes the standard input string by string, not character by character.

You now use the tr utility to change lowercase characters to uppercase, as well as replace colon characters with spaces.

# **To format using the grep and tr commands:**

+   1. Use the grep command to retrieve a record from the corp_phones file that matches the phone number 219-555-4501, and then pipe the output to tr to replace the colon characters in the record with space characters. Type the following command and then press Enter:

```
$ grep 219-555-4501 corp_phones | tr ':' ' '
```

Your screen looks similar to Figure 7-18.

![](bbox=[0.2, 0.53, 0.78, 0.82])

Figure 7-18: Output of grep and tr commands