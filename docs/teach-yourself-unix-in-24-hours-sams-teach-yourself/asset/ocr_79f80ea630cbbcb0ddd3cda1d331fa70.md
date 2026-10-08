# Hour 9

3. Space is critical in all wildcard patterns, too. Watch what happens if I accidentally add a space between the closing bracket of the range specification and the asterisk following:

```
% Is -Cfd [a-z] *
Archives/ bigfiles owl.c src/
InfoWorld/ News/ bin/ sample temp/
Mail/ OWL/ keylime.pie sample2 femme
```

This time, the shell tried to match all files whose names were one character long and lowercase, and then it tried to match all files that matched the asterisk wildcard, which, of course, is regular files in the directory.

4. The combination of character ranges, single-character wildcards, and multi-character wildcards can be tremendously helpful. If I move to another directory, I can easily search for all files that contain a single digit, or underscore in the name:

```
% cd Mail
% Is -Cf
71075.446 emilyc mailbox sartin
72033.216 gordon_hat manley sent
bncinerin harrism marmi shalini
bob_gill j=travel marv siob_n
cennamo james matt_ruby steve
dane_some jeffo tai
dataylor john_welch mwcilla taylor
decc john_prage netnetflix.postings v892127
diserti kca rat wcenter
druby lehman windows
dunlaplim lexb xdlf
eanuts mac rustle
```

```
% Is *[0-9]_*
71075.446 ean_uts matt.ruby x1f
72033.216 gordon_hat netnews.postings
bob_gill john_welcher siob_n
dane_some john_prage v892127
```

I think the best way to learn about pervasive features of UNIX such as filename wildcards is to use them. If you flip through this book, you immediately notice that the examples are built on earlier information. This will continue to be the case, and the filename range notation shown here will be used again and again, in combination with the asterisk and question mark, to specify groups of files or directories.

Remember that, if you want to experiment with filename wildcards, you can most easily use the echo command because it dutifully prints the expanded version of any pattern you specify.

![](bbox=[0.055, 0.875, 0.138, 0.966])